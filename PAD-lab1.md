## Agent de mesaje

Integrarea bazată pe agenți de mesaje care ar permite o comunicare asincronă
dintre componentele distribuite ale unui sistem

### Prerequisites

- VCS (Version Control System) Git;
- Limbajul de programare: nu este restricționat.
Însă, cu cît mai exotic este limbajul de programare,
cu atît sunt mai mari șansele că vor fi puse întrebări legate de particularitățile acestuia
(nimic grav, doar pentru a înțelege clar implementarea).
- Cunoștințe despre: git, protocoale de transport, agenți de mesaje (definiția, scopul, noțiuni de bază),
date semi-structurate (XML, JSON).

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

- Elaborarea protocolului de comunicare;
- Alegerea protocului de transport și argumentarea alegerii;
- Implementarea cozii de mesaje (utilizînd colecții de date concurente)

Implementează o coadă de mesaje care poate avea atît multipli productărori (expeditori) de mesaje, cît și multipli consumatori de mesaje.

![Coadă de mesaje](images/message-queue.gif)

Sistemul trebuie să permită:
- plasarea unui mesaj în coadă (concurent de mai mulți producători);
- consumarea mesajelor (concurent de mai mulți consumatori);
