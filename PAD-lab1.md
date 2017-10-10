## Agent de mesaje

Integrarea bazată pe agenți de mesaje care ar permite o comunicare asincronă
dintre componentele distribuite ale unui sistem

### Prerequisites

- VCS (Version Control System) Git - vezi [info din procesul de susținere](submission-process.md);
- Limbajul de programare: nu este restricționat.
Însă, cu cît mai exotic este limbajul de programare,
cu atît sunt mai mari șansele că vor fi puse întrebări legate de particularitățile acestuia
(nimic grav, doar pentru a înțelege clar implementarea).
- Cunoștințe despre: git, protocoale de transport, agenți de mesaje (definiția, scopul, noțiuni de bază),
date semi-structurate (XML, JSON).

Note:
- Informație despre git și linkuri utile găsești în [procesul de sustinere](submission-process.md);
- Pentru info despre agent de mesaje consultă urmatoarele surse:
    + [Distributed systems: principles and paradigms](https://moodle.ati.utm.md/pluginfile.php/5693/mod_glossary/attachment/8/distributed-systems-principles-and-paradigms-2nd-edition.pdf)
    4.3 MESSAGE-ORIENTED COMMUNICATION (p 159)
    + [Indicații metodice de pe moodle](https://moodle.ati.utm.md/mod/book/view.php?id=1613)

### Obiective

- Studiul agenților de mesagerie;
- Elaborarea unui protocol de comunicare al agentului de mesaje;
- Tratarea concurentă a mesajelor;
- Alegerea protocolului de transport (în dependență de scopul/domeniul de aplicare al agentului de mesaje);
- Alerea și elaborarea strategiei de păstrare a mesajelor;

### Sarcinile și baremul
Sarcina de bază este minim necesar pentru această lucrare de laborator.
Toate sarcinile reprezintă o continuitate. Adică, sarcina pentru nota 6 reprezintă cîteva sarcini care se vor baza pe sarcina pentru nota 5.

##### *Sarcina de bază* - Implementarea unei cozi de mesaje(nota 5)

[Demo (Clojure)](https://github.com/Alexx-G/pad-broker)
[Demo (Python)](https://github.com/Alexx-G/PAD-L1-demo)

- Elaborarea protocolului de comunicare.
Descrie protocolul într-un fișier [markdown](https://guides.github.com/features/mastering-markdown/)
și salvează-l în mapa „docs” din repozitoriul tău;
- Alegerea protocului de transport și argumentarea alegerii;
- Implementarea cozii de mesaje (utilizînd colecții de date concurente)

Implementează o coadă de mesaje care poate avea atît multipli productărori (expeditori) de mesaje, cît și multipli consumatori de mesaje.

![Coadă de mesaje](images/message-queue.gif)

Sistemul trebuie să permită:
- plasarea unui mesaj în coadă (concurent de mai mulți producători);
- consumarea mesajelor (concurent de mai mulți consumatori);

##### Implementarea mecanismului de stocare a mesajelor (Nota 6)

Stocarea mesajelor cu scopul asigurării robusteții cozii de mesaje. Adică, sistemul trebuie să:
- Serializeze coada de mesaje;
- Să o stocheze persistent (memorie secundară);
- În cazul întreruperii lucrului sistemului să restabilească (deserializeze) coada de mesaje din copia stocată.

##### Implementarea mecanismului de rutare a mesajelor (Nota 7)

Este necesar de a adăuga în sistem suportul la multiple cozi de mesaje (atît pentru producători, cît și pentru consumatori). Cît și a mecanismului de rutare a mesajelor la cozi.

![Content Based Routing](images/router.gif)

Cerințe concrete:
- Ajustarea protocolului agentului de mesaje cu scopul de a adăuga mecanismul de rutare;
- Adăugarea multiplelor cozi (de dorit să fie dinamic - în dependență de cererea producătorului);
- Consumarea dintr-o coadă non existentă trebuie să productă eroare explicită, prevăzută de protocol.

Bonus points (+1):
- Asigură compatibilitatea protocolului cu clienții din etapa precedentă (fără mecanism de rutare);
- Implementează cozi persistente și non-persistente. Acele persistente vor rămîne chiar după consumarea tuturor mesajelor, non-persistente se distrug după consumarea ultimului mesaj.

##### Implementarea patternului de publisher-subscriber (Nota 8)

Taskurile precedente presupun că consumatorul cerea explicit de fiecare dată un mesaj din coadă.
Iar însăși *coada* reprezenta un *buffer* de mesaje care avea o denumire pentru routing.
Pattern-ul publisher-subscriber permite consumatorului o singură dată să se „aboneze” (subscribe) la mesaje după un anumit criteriu (de exemplut *topic* mesajului),
și la apariția unui astfel de mesaj, dacă sunt consumatori, el este automat transmis consumatorilor respectivi.

Astfel, dispare necesitatea în cozi propriu-zise - mesajele sunt rutate după *topic* (la etapa precedentă denumirea cozii și avea rolul unui topic) și livrate consumatorilor care s-au abonat la *topic*-ul respectiv.

![Publisher Subscriber](images/pubsub.gif)

Rolul producătorului rămîne același (se schimbă doar denumirea).
Însă rolul consumatorului este mai simplu - el trebuie doar să se aboneze,
**să mențină conexiunea deschisă** și să aștepte mesaje respective.

- Ajustarea protocolului agentului de mesaje;
- Adăugarea mecanismului de abonare (subscribe);
- Abonarea la un topic inexistent (topic pentru care nu au fost expediate mesaje) trebuie să fie reflectată/tratată de către broker și clienți.

**Notă:** topic reprezintă un identificator al unui canal de comunicare între producători/abonați prin broker.
Rolul topic-ului este similar cu rolul cozilor din etapa precedentă - gruparea logică a mesajelor cu scopul rutării mai flexibile. Doar că topic-ul permite abstractizarea de la cozi ca mecanism de stocarea și nu impune restricții la implementarea acestuia.

**Notă 2:** Persistența în acest caz suferă schimbări. Persistența la etapele precedente era la nivel de cozi - menținerea cozilor în memorie chiar dacă mesajele au fost consumate. În acest caz are sens de trecut persistența la nivel de mesaje - păstrarea mesajelor care nu au fost transmise niciunui consumator (sau alte interpretări care au bază rațională).

##### Implementarea rutării avansate a mesajelor (Nota 9)

Pînă la această etapă, deși existau multiple topic-uri, atît producătorul cît și consumatorul puteau lucra doar cu unul.
Sarcina este de a adăuga posibilitatea rutării avansate a mesajelor (abonarea la multiple topic-uri).

Ajustează protocolul și implementează una următoarele sarcini:
- rutarea după topic (posibilitatea de a specifica un pattern);
- posiblitatea de a enumera explicit topic-urile;

Exemplu rutării după topic:
Să presupunem că convenția la dumele cozii e următoarea- `<numele companiei>.<numele produsului>.<tipul mesajelor - eroare, info, etc>`

Atunci, vor fi disponibile următoarele variații:
- `Google.*` - toate mesajele pentru toate produsele a companiei „Google”
- `Google.Nest.*` - toate mesajele pentru produsul „Nest” a companiei „Google”
- `Google.*.error` - toate messajele de tip „error” pentru compania „Google”
- `*.*.critical-erorr` - toate mesajele pentru toate companiile de tip „critical-error”
- etc.

Acesta e doar un exemplu. Puteți oferi posibilitatea de a specifica o expresie regulată (RegEx) la expediere/abonare.


##### Implementarea mecanismului „last will and testament” (Nota 10)

Mecanismul „last will and testament” (impementat în protocolul [mqtt](http://www.hivemq.com/blog/mqtt-essentials-part-9-last-will-and-testament))
este utilizat pentru a notifica despre deconectarea anormală abonatului (subscriber).
Adică, sunt situații cînd este necesar să cunoști dacă deconectarea abonatului a fost una așteptată sau nu. Însă pentru aceasta sistemul trebuie să deosebească noțiunea de deconectare planificată și anormală.

Sarcinile:
- Ajustează protocolul ca subscriberii, înainte de deconectare să transmită un mesaj specific;
- Ajustează protocolul ca subscriberii la conectare să transmită: mesajul și coada pentru „last will and testament”;
- Ajustează sistemul ca acesta să detecteze deconectări anormale și să transmită mesajul „last will and testament” (dacă este cazul).
