# 🧹 Module Clean Code
## Master 2 Data & Strategy

---

### 📋 Contenu du module

Ce module de **7 heures** (2 sessions de 3h30) couvre les bonnes pratiques d'écriture de code Python pour les projets data.

---

### 📁 Structure des supports

```
clean_code_module/
├── 📁 slides/
│   ├── CleanCode_Session1.pptx    # Slides Session 1
│   └── CleanCode_Session2.pptx    # Slides Session 2
├── 📁 notebooks/
│   ├── Session1_Notebook.ipynb    # TP Session 1 (à trous)
│   └── Session2_Notebook.ipynb    # TP Session 2 (à trous)
├── 📁 cheatsheets/
│   ├── Cheatsheet_Session1_Documentation.md
│   └── Cheatsheet_Session2_Pandas_Regex.md
├── 📁 data/
│   ├── campagne_marketing_ecommerce.csv
│   └── campagne_marketing_ecommerce.xlsx
└── README.md
```

---

### 🗓️ Organisation pédagogique

#### Session 1 (3h30) - Lire, comprendre et documenter du code

| Durée | Séquence | Support |
|-------|----------|---------|
| 20 min | Introduction : pourquoi le clean code ? | Slides 1-3 |
| 30 min | Naviguer dans la documentation | Slides 4 + Notebook |
| 45 min | Interpréter du code existant | Slides 5-6 + Notebook |
| 15 min | *Pause* | |
| 40 min | Commenter et documenter | Slides 7-8 + Notebook |
| 35 min | Structurer un projet multi-fichiers | Slide 9 + Notebook |
| 25 min | Exercice : ajouter une fonctionnalité | Notebook |

**Livrable** : Notebook legacy nettoyé et documenté

---

#### Session 2 (3h30) - Audit et analyse propre avec Pandas

| Durée | Séquence | Support |
|-------|----------|---------|
| 15 min | Rappel & présentation du dataset | Slides 1-2 |
| 35 min | Audit initial avec Pandas | Notebook |
| 40 min | Gestion des valeurs manquantes | Slides 3 + Notebook |
| 15 min | *Pause* | |
| 30 min | Sélection et filtrage avancés | Slides 4 + Notebook |
| 30 min | Expressions régulières | Slides 5-6 + Notebook |
| 30 min | Statistiques et présentation | Slides 7-8 + Notebook |
| 15 min | Synthèse & checklist | Slides 9-10 |

**Livrable** : Pipeline d'audit complet et reproductible

---

### 📊 Dataset

**Campagne marketing e-commerce** (~5150 lignes, 16 colonnes)

Problèmes de qualité intentionnels :

- Valeurs manquantes (~1500 cellules)
- Doublons (~150 lignes)
- Formats incohérents (dates, montants, téléphones)
- Emails invalides
- Texte à nettoyer avec regex

---

### 📚 Ressources complémentaires

**Documentation officielle :**

- [Python docs](https://docs.python.org)
- [Pandas docs](https://pandas.pydata.org/docs)
- [PEP 8 - Style Guide](https://peps.python.org/pep-0008/)
- [PEP 257 - Docstrings](https://peps.python.org/pep-0257/)

**Outils :**

- [Regex101](https://regex101.com) - Testeur de regex interactif
- [Black](https://github.com/psf/black) - Formateur automatique
- [Flake8](https://flake8.pycqa.org) - Linter PEP 8

**Livres :**

- *Clean Code* - Robert C. Martin
- *The Hitchhiker's Guide to Python* - Kenneth Reitz

---

### ⚙️ Prérequis techniques

```bash
pip install pandas numpy openpyxl jupyter
```

---

*Module développé pour le programme RNCP7 Data & Strategy*
