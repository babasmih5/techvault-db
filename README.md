# Proiectarea Bazelor de Date – Magazin Online de Componente și Periferice PC

**Student:** Babaș Mihai Sebastian

**Specializarea:** Calculatoare, Anul III

**An universitar:** 2026 – 2027  

---

## 1. Scopul și Descrierea Proiectului
Acest depozit conține proiectul semestrial realizat în cadrul disciplinei **Proiectarea Bazelor de Date** și vizează proiectarea conceptuală, logică și fizică, implementarea în SQL și integrarea cu o aplicație software și un modul de Inteligență Artificială a unei baze de date relaționale (normalizată în **FN3**) pentru un **magazin online de componente hardware și periferice pentru calculatoare**.

### Probleme rezolvate:
- **Gestiunea strictă a stocurilor și prevenirea *overselling*-ului** prin constrângeri de integritate și declanșatori (*triggers*).
- **Evidența structurată a catalogului hardware** (procesoare, plăci de bază, plăci video, memorii RAM, stocare SSD/HDD, surse, carcase, monitoare și periferice), a furnizorilor, brandurilor și perioadelor de garanție.
- **Analiză predictivă prin Machine Learning:** extragerea indicatorilor de achiziție printr-un *View* SQL dedicat, antrenarea unui model cu `scikit-learn` / `pandas` și salvarea predicțiilor înapoi în SGBD.

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
