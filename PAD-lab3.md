## Procesarea datelor distribuite semi-structurate

Scopul lucrării rezidă în studiul modelelor pentru procesarea datelor XML (DOM/ SAX) și JSON la distribuirea acestora.

### Prerequisites

- VCS (Version Control System) Git - vezi [info din procesul de susținere](submission-process.md);
- Cunoștințe despre: git, protocoale de transport, date semi-structurate (XML, JSON).
- Cunoștințe de bază despre sisteme distribuite - noțiune și caracteristici.
- Cunoștințe de bază despre t

Note:
- Informație despre git și linkuri utile găsești în [procesul de sustinere](submission-process.md);
- Pentru info despre sisteme distribuite consultă urmatoarele surse:
    + [Distributed systems: principles and paradigms](https://moodle.ati.utm.md/pluginfile.php/5693/mod_glossary/attachment/8/distributed-systems-principles-and-paradigms-2nd-edition.pdf)
    1.1 DEFINITION OF A DISTRIBUTED SYSTEM (p 2);
    1.2 GOALS
    + [Indicații metodice de pe moodle](https://moodle.ati.utm.md/mod/book/view.php?id=1727&chapterid=15)


### Obiective

- Aplicarea protocolului TCP în transmisiuni de date;
- Dezvoltarea unui sistem cu date distribuite eterogene și utilizarea unui mediator pentru accesarea acestora.
- Crearea unui modul de validare a datelor de format XML ce parvin centralizat de la nodul de mediere, Maven,  spre client.

### Sarcinile și baremul

##### Implementarea unui sistem cu date distribuite eterogene (nota 5)
Sarcina de bază este extinderea sistemului distribuit din laboratorul precedent prin eliminarea
UDP multicast și înlocuirea acestuia cu un mediator.
La fel se introduce transmiterea datelor folosind formate de date semi-structurate.

- Adăugarea mediatorului (sau „data warehouse” node - **în continuare W**) care va colecta datele
de la noduri informaționale și va comunica cu clientul;

##### Implementarea procedurii de lucru cu date eterogene și validarea XML (nota 6-7)
Scopul este de a lucra cu date eterogene: nodurile informaționale expun datele într-un format,
însă Mediatorul/W expune datele în alt format. Apare necesitatea de a combina
date cu format diferit.

- Nodurile informaționale serializează datele în JSON;
- Mediatorul/W serializează datele colectate în XML;
- Clientul validează datele primite folosing XML Schema Definition (XSD) sau DTD.

##### Eterogenizarea datelor la nodurile informaționale (nota 8)
La această etapă nodurile informaționale pot expune fie XML și JSON. Și Mediatorul/W
trebuie să fie extins pentru a putea agrega date eterogene și expune un format unic - XML.

- Nodurile informaționale expun datele în XML sau JSON;
- Mediatorul/W colectează și agreghează datele și le expune în formatul XML;

##### Implementarea posibilității de a cere datele într-un format anumit (nota 9)
Se cere adăugarea unui grad de flexibilitate mai mare în ceea ce privește formatul expus
de către Mediator/W. Adică, clientul trebuie să aibă posibilitatea de a solicita fie XML, fie JSON.

- Clientul poate specifica în ce format datele trebuie să fie reprezentate;
- Dacă clientul a solicitat XML, clientul aplică validarea implementată la etapele precedente;
- Mediatorul/W trebuie să serializeze datele colectate în dependență de formatul
solicitat de către client;

##### Validarea datelor în formatul JSON (nota 10)
La etapele precedente se valida doar răspunsul primit în formatul XML (fiindcă e standartizat).
Se cere validarea răspunsului primit în formatul JSON utilizînd JSON schema.

- Validarea datelor în formatul JSON de către client. Utilizînd [JSON Schema](http://json-schema.org/).
