## Protocolul HTTP: mijloc transport date distribuite

Studiul protocolului HTTP în contextul distribuirii datelor. Utilizarea metodelor HTTP în implementarea interacțiunii dintre client și un server de aplicații.

### Prerequisites

- VCS (Version Control System) Git - vezi [info din procesul de susținere](submission-process.md);
- Cunoștințe despre: HTTP
- Cunoștințe de bază despre sisteme distribuite - noțiune și caracteristici;
- Cunoștințe solide despre procesul de serializare/deserializare a obiectelor;

Note:
- Informație despre git și linkuri utile găsești în [procesul de sustinere](submission-process.md);
- Pentru info despre sisteme distribuite consultă urmatoarele surse:
    + [Distributed systems: principles and paradigms](https://moodle.ati.utm.md/pluginfile.php/5693/mod_glossary/attachment/8/distributed-systems-principles-and-paradigms-2nd-edition.pdf)
    12 DISTRIBUTED WEB-BASED SYSTEMS p.545
    + [Indicații metodice de pe moodle](https://moodle.ati.utm.md/mod/book/view.php?id=1717)


### Obiective

- Aplicarea protocolului HTTP în transmisiuni de date;
- Elaborarea unui sistem cu procesare concurentă a cererilor HTTP;

### Sarcinile și baremul

##### Implementarea unui sistem cu date distribuite eterogene (nota 5-6)
Sarcina de bază este extinderea sistemului distribuit din laboratorul precedent adăugarea
nodului **data-warehouse** (depozitul de date) și înlocuirea transportării datelor
prin TCP cu HTTP.

- Adăugarea **data warehouse** (dacă în laboratorul precedent a fost elaborat mediator);
- Utilizarea protocolului HTTP pentru a transmite datele
    + clientul va utiliza metoda **GET** pentru a obține datele de la **data warehouse**;
    + nodurile informaționale vor transmite datele către **data warehouse** utilizînd
    metoda **PUT**;
- Clientul poate solicita atît o listă de obiecte, cît și un singur obiect prin identificator.
Dacă **data warehouse** nu are obiectul solicitat, se întoarce răspunsul cu codul respectiv.
