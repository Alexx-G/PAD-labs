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

##### Îmbunătățirea configurabilității sistemului distribuit (nota 7)

- Preluarea configurației sistemului distribuit dintr-un fișier de configurații.
Astfel va fi posibil de schimbat schema sistemului distribuit doar modificînd
un singur fișier cu configurația acestuia.

##### Elaborarea și implementarea unui simplu limbaj de interogări (nota 8)
Posibilitatea de a procesa parțial colecția distribuită de date pe nodurile informaționale.
Adică, nodurile informaționale trebuie să accepte construcții specifice, pentru
a efectua operații sortare, filtrare sau grupare nemijlocit pe nodurile informaționale.
Se acceptă orice [DSL](https://en.wikipedia.org/wiki/Domain-specific_language)
, începînd de la simplu dicționar pînă la pseudo-SQL.

Cerințe către sistem:
- Oferirea interfeței de interogare a nodurilor cu cel puțin una din operații
    - filtrare,
    - sortare,
    - grupare

##### Înlocuirea UDP multicast cu un mediator/broker (nota 9-10)
Folosind UDP pentru a determina nodul principal, sistemul devine susceptibil la
pierderi de date + problema firewall-urilor. Pentru a rezolva această problemă,
se propune introducerea unui nou component intermediar (mediator/broker), care
va lucra folosind TCP și va garanta comunicarea sigură între client și DIS.

#### Structuri DIS

Alege structura în dependență de numărul ordine.

![Structuri DIS](images/dis-structures.jpg)
