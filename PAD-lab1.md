## Agent de mesagerie

Integrarea bazată pe agenți de mesaje care ar permite o comunicare asincronă
dintre componentele distribuite ale unui sistem

### Prerequisites

#### VCS (Version Control System) (Git)

Drept VCS va fi utilizat Git. Ca provider de serviciu va fi utilizat github.com
Utilizarea VCS are ca scopuri:
- transparența în implementarea proiectului;
- colaborarea eficientă;
- facilizarea revizuirii proiectului.

Referințe:
- Instalarea clientului git;
- Configurarea cheilor;
- Principii de bază;
- Utilizarea eficientă a git-ului (git flow);

#### Alegerea stack-ului tehnologic

Nu este restricție în utilizarea unui limbaj de programare.
Însă, cu cît mai exotic este limbajul de programare,
cu atît sunt mai mari șansele că vor fi puse întrebări legate de particularitățile acestuia
(nimic grav, doar pentru a înțelege clar implementarea).

Utilizarea completă a soluțiilor existente nu este admisibilă.
Însă utilizarea unor librării care facilitează rezolvarea unei
probleme concrete este complet ok.
De ex: Dacă modulul built-in a limbajului ales nu oferă o interfață comodă pentru a lucra cu
parsarea XML, însă există un third-party modul care oferă o interfață comodă, atunci utilizarea acestuia este binevenită.

### Obiective

- Studiul agenților de mesagerie;
- Elaborarea unui protocol de comunicare al agentului de mesaje;
- Tratarea concurentă a mesajelor;
- Alegerea protocolului de transport (în dependență de scopul/domeniul de aplicare al agentului de mesaje);
- Alerea și elaborarea strategiei de păstrare a mesajelor;

### Sarcinile și baremul
