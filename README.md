# Proiectarea Bazelor de Date – Magazin Online de Componente și Periferice PC

**Student:** Babaș Mihai Sebastian  
**Specializarea:** Calculatoare, Anul III  
**Cadru didactic îndrumător:** Văduva Bogdan  
**An universitar:** 2026 – 2027  

---

## 1. Descrierea Proiectului
Acest depozit conține proiectul realizat la disciplina **Proiectarea Bazelor de Date**. Proiectul constă în proiectarea și implementarea unei baze de date relaționale (normalizată în **FN3**) pentru un **magazin online de componente și periferice PC**, alături de o aplicație CRUD și un script de învățare automată.

### Ce urmărește baza de date:
- **Gestiunea catalogului de produse:** evidența componentelor (procesoare, plăci de bază, plăci video, memorii RAM, SSD/HDD, surse, carcase și periferice), a categoriilor, producătorilor, furnizorilor și perioadelor de garanție.
- **Controlul stocurilor și al comenzilor:** verificarea stocului disponibil la plasarea comenzilor și păstrarea prețului de achiziție în liniile comenzii (`detalii_comanda`), astfel încât modificările ulterioare de preț din catalog să nu afecteze comenzile vechi.
- **Integrarea cu un model Machine Learning:** extragerea datelor de vânzări în Python (`pandas`, `scikit-learn`), antrenarea unui model simplu și salvarea rezultatelor într-un tabel dedicat din baza de date.

---

## 2. Structura Depozitului Git

```text
techvault/
├── README.md
├── .gitignore
├── docs/
├── techvault-db/
│   ├── schema/
│   ├── seed/
│   ├── views/
│   ├── procedures/
│   ├── queries/
│   └── diagrams/
├── app/
└── tests/
```

---

## 3. Proiectarea Bazei de Date

### 3.1. Analiza cerințelor și regulile de business
Pentru proiectarea bazei de date a magazinului de componente și periferice PC, s-au stabilit următoarele cerințe și reguli pe care sistemul le respectă prin maparea directă pe entități:

- **Identificare unică (Catalog):** Entitatea **PRODUSE** identifică fiecare articol printr-un ID intern și un cod unic SKU (de exemplu, `CPU-AMD-5600X`), având asociate o denumire, un preț de vânzare și cantitatea curentă din stoc.
- **Încadrare și Origine:** Orice înregistrare din entitatea **PRODUSE** aparține obligatoriu unei singure înregistrări din entitatea **CATEGORII** (ex. procesoare, plăci de bază) și provine de la o entitate **PRODUCATORI** (AMD, Intel, ASUS etc.).
- **Aprovizionare și garanție:** Stocurile pentru **PRODUSE** sunt asigurate de entitatea **FURNIZORI**, identificați prin CUI unic și date de contact. Pentru fiecare componentă se reține perioada de garanție în luni.
- **Restricții de valori:** Prețul din **PRODUSE** trebuie să fie strict mai mare decât 0, iar stocul curent nu poate scădea sub 0.
- **Securitate și Clienți:** Datele de acces, rolurile (admin, operator, client) și parolele hash sunt gestionate de entitatea **UTILIZATORI**. Fiecare cumpărător are un profil comercial în entitatea **CLIENTI**, identificat prin nume, telefon, oraș și e-mail unic (legat opțional de un cont de utilizator).
- **Structura tranzacțiilor:** Entitatea **CLIENTI** poate plasa una sau mai multe înregistrări în entitatea **COMENZI**. O comandă stochează data, statusul curent (`In asteptare`, `Confirmata`, `Expediata`, `Livrata`, `Anulata`) și metoda de plată.
- **Liniile comenzii și istoricul prețurilor:** Relația mulți-la-mulți dintre tranzacții și catalog este rezolvată de entitatea asociativă **DETALII_COMANDA**. Aici se salvează produsele dintr-o comandă, cantitatea (minimum 1), dar mai ales prețul unitar și discountul la momentul achiziției, astfel încât fluctuațiile de preț din entitatea **PRODUSE** să nu modifice facturile vechi.
- **Evaluări:** Entitatea **CLIENTI** poate acorda note și comentarii textuale pentru articolele din **PRODUSE**, informații stocate în entitatea **RECENZII** (notă validată prin constrângere `CHECK` între 1 și 5).
- **Integrarea cu Inteligența Artificială:** Pe baza istoricului extras, scriptul Python (`app/main.py`) încadrează fiecare înregistrare din **CLIENTI** într-un segment de achiziție, salvând rezultatul (segmentul și scorul) în entitatea dedicată **PREDICTII_AI**.

### 3.2. Modelul ER

<img width="1024" height="572" alt="Diagrama" src="https://github.com/user-attachments/assets/17b498de-727d-4144-83da-4079d5b7b782" />