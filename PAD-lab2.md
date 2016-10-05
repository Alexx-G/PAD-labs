## Colecții distribuite de date

Scopul lucrării de laborator rezidă în studiul protocoalelor de transport TCP/IP în contextul dezvoltării unei aplicații conținând colecții distribuite de date.

### Prerequisites

- VCS (Version Control System) Git - vezi [info din procesul de susținere](submission-process.md);
- Cunoștințe despre: git, protocoale de transport, date semi-structurate (XML, JSON).

### Obiective

- Aplicarea protocolului UDP în transmisiuni unicast și multicast;
- Aplicarea protocolului TCP în transmisiuni de date;
- Procesarea colecțiilor de obiecte.

### Sarcinile și baremul

##### Implementarea unui sistem informațional ce oferă colecții distribuite de date (nota 5)

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
