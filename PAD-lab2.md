## Colecții distribuite de date

Scopul lucrării de laborator rezidă în studiul protocoalelor de transport TCP/IP în contextul dezvoltării unei aplicații conținând colecții distribuite de date.

### Prerequisites

- VCS (Version Control System) Git - vezi [info din procesul de susținere](submission-process.md);
- Cunoștințe despre: git, protocoale de transport, date semi-structurate (XML, JSON).
- Cunoștințe de bază despre sisteme distribuite - noțiune și caracteristici.

Note:
- Informație despre git și linkuri utile găsești în [procesul de sustinere](submission-process.md);
- Pentru info despre sisteme distribuite consultă urmatoarele surse:
    + [Distributed systems: principles and paradigms](https://moodle.ati.utm.md/pluginfile.php/5693/mod_glossary/attachment/8/distributed-systems-principles-and-paradigms-2nd-edition.pdf)
    1.1 DEFINITION OF A DISTRIBUTED SYSTEM (p 2)
    1.2 GOALS
    + [Indicații metodice de pe moodle](https://moodle.ati.utm.md/mod/book/view.php?id=1648)


### Obiective

- Aplicarea protocolului UDP în transmisiuni unicast și multicast;
- Aplicarea protocolului TCP în transmisiuni de date;
- Procesarea colecțiilor de obiecte.

### Sarcinile și baremul

##### Implementarea unui sistem informațional ce oferă colecții distribuite de date (nota 5-6)

- Elaborarea protocolulului de comunicare între client și sistem informațional distribuit;
- Elaborarea și implementarea nodului informațional;
- Determinarea nodului principal utilizînd UDP multicast;
- Interogarea nodului principal selectat utilizînd TCP;
- Stabilirea legăturilor între noduri informaționale și interogarea
„legăturilor” de către nodul principal.
