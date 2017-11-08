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
- Utilizarea posibilităților oferite de HTTP pentru implementarea unor funcționalități mai avansate a sistemului.

### Sarcinile și baremul

##### Informații generale
- Se permite utilizarea framework-urilor pentru **data-warehouse**;
  **DAR**, este binevenită utilizarea soluțiilor de tip constructor/micro-frameworks.
- Componentele diferite pot fi implementate utilizînd platforme/limbaje diferite;
- Clientul la etapa aceasta, poate fi atît o aplicație implementată separat cît și un instrument existent (e.g. `curl`).

**Pentru echipe**
- **Fiecare** membru trebuie să aibă contribuție la proiectul final;
- Implementarea aplicației client se accepta ca task separat pentru un membru a echipei, cu condiția că clientul este **suficient** de complicat;
- În caz că se aplică tehnicile **DevOps** se acceptă aceasta la fel să fie un task separat.

##### Implementarea unui sistem cu date distribuite eterogene (nota 5-6)
Sarcina de bază este crearea nodului **data-warehouse** (depozitul de date) 
și utilizarea protocolului HTTP pentru transport de date.

- Crearea unui nod **data warehouse**
  - Datele pot fi stocate în memorie fără utilizarea unui DBMS
  - Definirea a **cel puțin 2 resurse** (E.g. Angajat și Departament)
- Implementarea RESTful API pentru resursele definite
  - Interfața trebuie să expună **cel puțin 3 operațiuni** (list, retrieve, create)
    - Opțional tot setul de operțiuni (S)CRUD pentru toate resursele
  - Să se utilizeze metodele, codurile de răspuns și antetele **conform specificației**

##### Utilizarea GET query string pentru paginare și filtrare (nota 7)
Să se utilizeze *query string* pentru a oferi clientului posibilitatea de a specifica parametrii de **filtrare** și **paginare** a datelor returnate de endpoint-ul *list*.

- Filtrare
  - Căutarea prin cîmpuri textuale relevante (E.g. `/api/students/?q=John`)
  - Filtrarea mai complexă per cîmp
    (E.g. `/api/students/?first_name__startswith=J` or `/api/students/?avg__gte=9`)
- Paginarea bazată fie pe *offset-uri și limite* sau pe *pagini*.

##### Validarea entităților expediate de client conform schemei/constrângerilor (nota 8)
Pentru operațiuni de *creare și editare*, sistemul trebuie să valideze datele expediate de client conform unei scheme/constrîngerilor și, în caz de eroare, să returneze răspunsul respectiv.

Dacă datele expediate de client prin **POST** sau **PUT** nu sunt valide, 
răspunsul returnat de sistem **trebuie**
- să returneze codul **400 BAD REQUEST**;
- să specifice în body a răspunsului ce cîmpuri/constrînger **nu sunt valide**.

##### Content negotiation & HATEOAS (nota 9)

###### Content negotiation
Implementarea mecanizmului care va permite in baza header-ului `Accept`, 
specificat de client, să returneze reprezentarea resursei în formatul solicitat.

- În header-ul `Accept` clientul poate specifica mai multe formate,
  în ordinea preferinței. [Accept in RFC](https://tools.ietf.org/html/rfc2616#section-14.1)
- Dacă sistemul nu suportă formatul specificat de către client, 
  sistemul *ar trebui* să returneze răspunsul **406 NOT ACCEPTABLE**.
- Sistemul **trebuie** să suporte următoarele formate **json, xml, html/yaml**
- Header-ul `Content-Type` a răspunsului va specifica ce format a primit clientul.


###### HATEOAS (Hypermedia As The Engine Of Application State) 
Implementarea de HATEOAS pentru datele returntate anterior.

##### Sincronizarea datelor între 2 sau mai multe noduri data-warehouse (nota 10)
Adăugarea a cel puțin încă unui nod **data-warehouse** în sistem.
Astfel, sistemul distribuit va fi format din 2+ noduri data-warehouse 
și clientul va putea alege cu ce nod să interacționeze. 
Nodurile vor conține aceleași date și vor sincroniza datele între ele, dacă clientul modifică/adaugă o entitate.

- Crearea si configurarea a nodurilor existente pentru sincronizare;
  - Automatizarea deployment-ului a nodurilor.
- Implementarea mecanizmului de sincronizare,
  ce ne permite reflectarea automata a schimbarilor de pe un nod pe altele.
  - Să se rezolve problema modificării aceleași entități pe 2 noduri concomitent.
