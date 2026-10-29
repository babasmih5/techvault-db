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
Pentru proiectarea bazei de date a magazinului de componente și periferice PC, s-au stabilit următoarele cerințe și reguli pe care sistemul trebuie să le respecte:

- **Identificare unică:** Fiecare produs este identificat printr-un ID intern și un cod unic SKU (de exemplu, `CPU-AMD-5600X` sau `GPU-RTX-4060`), având asociate o denumire, un preț de vânzare și cantitatea din stoc.
- **Încadrare în catalog:** Orice produs aparține obligatoriu unei singure categorii (procesoare, plăci de bază, plăci video, memorii RAM, SSD/HDD, surse, carcase, periferice) și unui producător (AMD, Intel, ASUS, Kingston, Logitech etc.).
- **Aprovizionare și garanție:** Produsele sunt aprovizionate de la furnizori identificați prin CUI unic și date de contact. Fiecare produs are o perioadă de garanție exprimată în luni (de exemplu, 24 sau 36 de luni).
- **Restricții de valori:** Prețul unui produs trebuie să fie strict mai mare decât 0, iar stocul curent nu poate scădea sub 0.
- **Înregistrarea clienților:** Fiecare client este înregistrat cu nume, prenume, număr de telefon, oraș și o adresă de e-mail unică în baza de date.
- **Structura comenzilor:** Un client poate plasa una sau mai multe comenzi. O comandă conține data plasării, starea curentă (`In asteptare`, `Confirmata`, `Expediata`, `Livrata`, `Anulata`) și metoda de plată (`Card`, `Ramburs`, `Ordin de plata`).
- **Liniile comenzii și păstrarea prețului:** O comandă poate include mai multe produse diferite, iar același produs poate apărea pe mai multe comenzi. În tabelul de legătură (`detalii_comanda`) se salvează cantitatea comandată (minimum 1), prețul unitar de la momentul achiziției și discountul aplicat, astfel încât modificările ulterioare de preț din tabelul `produse` să nu modifice valoarea comenzilor vechi.
- **Recenzii:** Clienții pot lăsa recenzii produselor, acordând o notă între 1 și 5 (validată prin constrângere `CHECK`) și un comentariu text.
- **Integrarea cu modelul de învățare automată:** Pe baza istoricului de comenzi extras din baza de date, scriptul Python (`app/main.py`) încadrează clienții pe segmente de achiziție și salvează rezultatul și scorul predicției în tabelul `predictii_ai`.

### 3.2. Modelul ER

<img width="2022" height="1381" alt="Fotografie" src="https://github.com/user-attachments/assets/93ecaa5a-9d46-434d-85b0-56418683d8d3" />

