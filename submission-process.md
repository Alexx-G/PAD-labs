## Susținerea laboratoarelor

*Nota: Rapoartele pot fi expediate in limba franceza/romana/engleza, dar numai in .PDF format.
Limba în care este scris raportul, nu influiențează nota finală.*

## Cerințe

- Vii la laborator deja informat despre sarcinile acestuia;
- Codul sursă a proiectului trebuie să fie păstrat pe GitHub;
Dacă lucrările de laborator reprezintă o continuitate,
atunci e suficient un singur repozitoriu, însă fiecare laborator va avea ramură (branch) de bază aparte. Master conține ultima versiune stabilă, anume master se va analiza în timpul susținerii.
- Proiectele cu un singur commit (sau foarte puține) nu se acceptă, sau se acceptă cu condiția atenției triple la susținere;
- Raportul trebuie să fie expediat în formatul **PDF**.
- Raportul trebuie să conțină (template în LaTeX în acest repo):
    - Pagina de titlu;
    - Obiectivele laboratorului;
    - Lista de task-uri implementate;
    - Explicatiile necesare despre modul in care au fost implementate task-urile (adauga referintele necesare);
    - Screenshot-urile care le consideri adecvate raportului (dacă sunt);
    - Concluzii - scurt (fără exagerări, minim 2-3 fraze complexe) și clar despre rezultatele obținute;
    - Bibliografie (dacă este)
    - Titlul fisierului **PDF** trebuie să fie în formatul
    `<Grupa>_<Nume>_<Prenume>_PAD.pdf`
- Proiectul trebuie să aibă structură rezonabilă. Diferă de la platformă la platformă, însă mai jos este descrierea generică.
- Instrucțiuni de asamblare (dacă sunt necesare) și rulare a proiectului;

## Procesul de elaborare a laboratorului

Tot laboratorul se împarte în 3 părți:
- Un mic test la începutul laboratorului, pe cunoașterea materialului acestuia;
- O sarcină de bază (demonstrarea unui minim necesar de cunoștințe pentru acest laborator);
- Sarcini adiționale;

Sunt 2 opțiuni de a susține laboratorul:
- Testul dat satisfăcător + sarcina de bază implementată **în timpul** laboratorului garantează nota 5. Îți rămîne doar să faci raportul și să-l expediezi conform descrierii de mai jos.
- Testul + sarcina de bază (de dorit în timpul laboratorului, pentru a obține consultații) + sarcinile opționale,
se vor aprecia conform baremului pentru lucrarea de laborator în cauză.
Îți rămîne să faci raportul, să-l expediezi și **să-l susții** (o procedură în care analizăm împreună lucrarea și o apreciem obiectiv).

### Implementarea soluției
Utilizarea completă a soluțiilor existente nu este admisibilă.
Însă utilizarea unor librării care facilitează rezolvarea unei
probleme concrete este complet ok.
De ex: Dacă modulul built-in a limbajului ales nu oferă o interfață comodă pentru a lucra cu
parsarea XML, însă există un third-party modul care oferă o interfață comodă, atunci utilizarea acestuia este binevenită.

#### GIT (VCS - version control system)
Drept VCS va fi utilizat Git. Ca provider de serviciu va fi utilizat [github.com](https://github.com)
Utilizarea VCS are ca scopuri:
- transparența în implementarea proiectului;
- colaborarea eficientă;
- facilizarea revizuirii proiectului.

Procesul de lucru:
- Te întregistrezi pe github;
- Creezi un repozitoriul nou (alegi .gitignore conform stack-ului tehnologic utilizat).
[More info](http://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#Ignoring-Files)
- Clonezi repozitoriul pe calculatorul tău;
- Adaugi un README.md file cu denumirea obiectului și proiectului;
- [Faci commit](https://help.github.com/articles/adding-a-file-to-a-repository-from-the-command-line/)
- Structurezi proiectul (conform descrierii de mai jos);
- Commit and push to master;
- Faci un branch nou pentru laboratorul respectiv si te schimbi pe dinsul (`man git-checkout`);
- Continui implementarea, făcînd commit-uri la fiecare pas logic (dar nu mai mult de 3 fișiere sau 50 lines of code într-un commit);
- La fiecare etapă semnificativă, push la ramura curentă pe server (dacă ai conexiune la internet).
Scopul este ca pe server să ai ultipa copie a lucrului tău;
- Dacă este necesar, adaugă descrierea la instrucțiuni/use-case-uri specifice și altă informație utilă despre implementare în cauză în README.md;
- La finisarea lucrării, fă „merge” la schimbările din ramura laboratorului în master. Apoi fă un [tag nou](https://git-scm.com/book/en/v2/Git-Basics-Tagging) care să aibă denumirea `L<nr lab>` și push la master pe server;

Astfel procesul tău de lucru va fi transparent la maxim și colaborarea în proiect va fi posibilă foarte ușor.

**Referințe:**
- [Instalarea clientului git](https://git-scm.com/downloads);
- [Configurarea cheilor](https://help.github.com/articles/generating-an-ssh-key/);
- Principii de bază
[Getting started](http://www.manniwood.com/starting_a_project_with_git.html)
[Git Book](http://www-cs-students.stanford.edu/~blynn/gitmagic/)
[Git Tutorial](http://www.vogella.com/articles/Git/article.html);
- Utilizarea eficientă a git-ului (
[git flow](http://nvie.com/posts/a-successful-git-branching-model/) and
[git book](http://git-scm.com/book));
- [Alte VCS](https://biz30.timedoctor.com/git-mecurial-and-cvs-comparison-of-svn-software/).

#### Structurarea proiectului
Dacă platforma aleasă are o structură recomandată, atunci aceasta trebuie folosită.
În caz contrar structura trebuie să fie următoarea:
```
.
├── .gitignore <-- gitignore specific for the project
├── README.md <-- readme of the project
├── requirements <-- folder with readme for project specific requirements
└── src <--- folder with source code
```

Nu ezitați să vă consultați dacă nu sunteți siguri la acest capitol.

#### Expedierea raportului și susținerea
După ce ai implementat task-urile și ai făcut raportul, asigură-te că în repozitoriul se află versiunea actuală a proiectului pe master, trimite-mi un e-mail:
- Atașează raportul în formatul **PDF**,
- Subiectul email-ului `[PAD][<grupa>][Lab<nr lab>][Nume Prenume]`,
- Linkul către repozitoriul cu lucrarea de laborator,
- Adresa destinatarului: utm-labs@gavrisco.com

Note:
- Prezentarea laboratorului în Latex nu este obligatorie(dar se va aprecia cu +1), se poate de prezentat și in varianta simplă PDF
- Cu cît mai multe detalii vei atașa la laboratorul tău, cu atît mai puține întrebari îți voi adresa in timpul prezentării.
- Dacă careva din noțiuni/cuvinte nu îți sunt cunoscute - google it.
- Dacă ai careva întrebări și nu le-ai găsit pe net, întreabă de colegii tăi.
- Dacă nici una din opțiuni nu lucrează pentru tine, expediază-mi un email cu întrebarea ta. Totuși, te-aș sfătui sa găsești singur ieșire din situație, asta te va ajuta in viitoarea ta carieră.
- Majoritatea noțiunilor si a documentației va fi in limba engleză, pentru a facilita verificarea acesteia.
