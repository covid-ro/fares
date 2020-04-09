# Face Recognition Server

**FaReS** este un server simplu de recunoastere a fetelor care expune doar un API utilizatorilor.
Pana in acest moment doar Ubuntu 18.04.4 LTS este o platforma suportata. Mai multe teste sunt in curs de
desfasurare.

Currently only romanian version of this document exists. English translation will follow soon.


## Continut
- [Introducere](#1-introducere)
- [Modificari; versiuni; TODO](#2-modificari-versiuni-todo)
- [Pregatire sistem si instalare](#3-pregatire-sistem-si-instalare)
- [Rulare server **FaReS**](#4-rulare-server-fares)


## 1. Introducere
**FaReS** este un server de aplicatii care poate fi utilizat pentru:
- a detecta fete din imagini sau
- a realiza **doar** comparatia a doua fete aflate fiecare in cate o imagine.

Implementarea are cateva limitari legare de performanta algoritmilor pe procesoare generice si pe GPU.
- imagini cu dimensiunea de max 1MB
- imagini care sa aiba latura cea mai mare de maxim 1280 pixeli
- o singura fata per imagine pentru operatia de comparatie

Pentru a rula acest server este nevoie de:
- un sistem fizic sau virtual cu Linux - Ubuntu 18.04.4 LTS si optional cu placa grafica NVIDIA si biblioteci CUDA
- python3
- module pentru python3
- nginx (recomandat) pentru a rula un server public

In arhivele din sectiunea [**Releases**](https://github.com/covid-ro/fares/releases) este inclusa si documentatia completa pentru API. Procedura de instalare este
detaliata mai jos.



## 2. Modificari; versiuni; TODO

#### [1.0.0] - 2020-03-31
Versiunea initiala a serverului. Contine API pentru comparatia a doua fete.


#### [1.1.0] - 2020-04-05

Actualizare API cu o metoda noua pentru detectarea fetei ('detect') si
diverse modificari minore.

##### Adaugat:
- adaugare endpoint detectie fete ('detect')
- corectata si actualizata documentatia

##### Modificari:
- endpoint 'recognize' marcat ca deprecated
- refactoring in module pentru operatiile de detectie si comparatie
- modificat clientul exemplu si convertit in unul pentru detectie si unul pentru comparatie

##### Probleme rezolvate:
- corectata documentatia


#### [1.1.1] - 2020-04-07

Adaugata aplicatie demo IOS.

##### Adaugat:
- arhiva aplicatie demo IOS


#### [1.1.2] - 2020-04-09

Adaugata aplicatie demo Android.

##### Adaugat:
- arhiva aplicatie demo Android


### TODO
- [x] adaugare enpoint pentru apel detectie fete in imagini
- [X] aplicatii exemplu de captura si prelucrare pentru ~~Android~~ si ~~IOS~~
- [ ] adaugarea posibilitatii de a descarca fetele gasite
- [ ] adaugare documentatie pentru integrarea cu nginx
- [ ] adaugare model de recunoastere a fetei CNN
- [ ] migrarea catre un server scris in C++ pentru a imbunatati performanta
- [ ] adaugarea unui endpoint cu unul sau mai multe fete pentru a le gasi in alta imagine
- [ ] adaugarea comparatiei de features, fara a mai face si detectia fetelor



## 3. Pregatire sistem si instalare

Serverul FaReS poate fi descarcat din sectiunea Releases a proiectului de pe GitHub. Documentatia se afla in arhiva, in directorul docs.

Instalarea este detaliata in prima parte a fisierului [INSTALL.md](INSTALL.md).



## 4. Rulare server **FaReS**

Rularea serverului este detaliata in partea a doua a fisierului [INSTALL.md](INSTALL.md).



## 5. Performanta si limitari

**Performanta**
FaReS realizeaza o comparatie intre doua imagini cu dimensiunea de 2400x3200 folosind CPU intr-un interval de pana la ~6-9 secunde. Pentru imagini cu dimensiune redusa (600x600) dureaza folosind tot CPU ~2-3 secunde. Timpul se injumatateste la utilizarea accelerarii GPU, insa imaginile trebuie sa aiba maximum 1000-1200 pixeli pe latura cea mai mare.

Estimarea pentru limitele solutiei private folosind CPU sunt, pe un sistem virtual cu 8 core-uri, de minim 5000 de comparatii pe ora.

Conform documentelor publice, acuratetea recunoasterii fetelor este:
- om: ~99.5% (TBD: de regasit sursa informatiei si adaugat)
- biblioteci folosite de server FaReS: 99.38% pe testul LFW (Labeled Faces in the Wild)

**Limitari** 
Implementarea FaReS are urmatoarele limitari:
- o singura fata per imagine
- pozitie verticala a fetei (se recomanda permiterea unei deviatii de 10 grade stanga-dreapta)
- dimensiunea laturii mari a imaginii de maximum 1300 de pixeli
- dimensiunea unei imagini de maximum 1 MB
- imaginile sunt transmise printr-un apel al unui API, imaginile fiind transmise encodate BASE64, in json
- nu se poate face diferenta intre o fotografie a unei persoane si fotografia unui ecran sau a unei fotografii


## 6. Integrare

Pentru integrarea intr-un sistem de productie se recomanda urmatorul proces:
1. Operatii efectuate pe _edge device_ (eventual cu indicatii pentru utilizator pentru a avea o imagine cu iluminare cat mai buna daca e vorba despre un telefon mobil):
- redimensionarea imaginilor prin prelucrare in mediu extern (dispozitiv cu camera, server API)
- verificarea imaginilor pentru a determina numarul de fete si a restrictiona imaginea la una singura (pe dispozitiv cu camera de preferat)
- verificarea luminozitatii imaginii
- eventuala conversie a imaginii la grayscale

In sectiunea [**Releases**](https://github.com/covid-ro/fares/releases) exista aplicatii demo pentru Android si IOS care exemplifica un asemenea flow.

2. Trimiterea catre serverul FaReS a imaginilor de comparat:
- de pe _edge device_ este primita imaginea
- se genereaza un JSON pentru request, care sa contina imaginea de baza si imaginea de comparat
- se trimite la server
- se primeste raspuns

3. Dupa comparatie:
- campul `match` din raspuns ofera informatii referitoare la similaritatea fetelor comparate
- se recomanda validarea umana la scaderea gradului de incredere sub un prag (peste 0.55-0.58 de exemplu, limita de detectie fiind la 0.6) si daca nu a fost gasita aceeasi persoana


