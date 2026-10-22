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
├── CHANGELOG.md
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
