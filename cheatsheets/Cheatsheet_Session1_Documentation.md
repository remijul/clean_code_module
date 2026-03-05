# 📚 Cheatsheet Clean Code - Session 1
## Documentation et Bonnes Pratiques Python

---

## 1. Accéder à la documentation

| Méthode | Usage | Exemple |
|---------|-------|---------|
| `help(obj)` | Documentation complète | `help(pd.DataFrame.merge)` |
| `obj?` | Documentation Jupyter | `pd.read_csv?` |
| `obj??` | Code source (si dispo) | `my_function??` |
| `dir(obj)` | Liste des attributs | `dir(pd.DataFrame)` |

**Ressources en ligne :**
- Python : [docs.python.org](https://docs.python.org)
- Pandas : [pandas.pydata.org/docs](https://pandas.pydata.org/docs)
- NumPy : [numpy.org/doc](https://numpy.org/doc)

---

## 2. Conventions de nommage (PEP 8)

| Type | Convention | Exemple |
|------|------------|---------|
| Variables | snake_case | `user_name`, `total_amount` |
| Fonctions | snake_case | `calculate_revenue()` |
| Classes | PascalCase | `DataProcessor`, `UserAccount` |
| Constantes | UPPER_SNAKE | `MAX_RETRIES`, `API_KEY` |
| Modules | snake_case | `data_loader.py` |
| Privé | _préfixe | `_internal_method()` |

**À éviter :**
- `x`, `temp`, `data2` → Préférer des noms explicites
- `l`, `O`, `I` → Confusion avec 1 et 0

---

## 3. Docstrings NumPy Style

```python
def calculate_revenue(transactions, tax_rate=0.2):
    """
    Calcule le revenu total après application de la taxe.
    
    Parameters
    ----------
    transactions : pd.DataFrame
        DataFrame contenant les colonnes 'amount' et 'quantity'.
    tax_rate : float, optional
        Taux de taxe à appliquer (default: 0.2).
    
    Returns
    -------
    float
        Revenu total après taxe.
    
    Raises
    ------
    ValueError
        Si tax_rate est négatif.
    
    Examples
    --------
    >>> df = pd.DataFrame({'amount': [100, 200]})
    >>> calculate_revenue(df, tax_rate=0.1)
    330.0
    
    Notes
    -----
    Le calcul exclut les montants négatifs.
    """
    pass
```

---

## 4. Anti-patterns à éviter

| Anti-pattern | ❌ Mauvais | ✅ Bon |
|--------------|-----------|--------|
| Magic numbers | `if status == 3:` | `if status == STATUS_ACTIVE:` |
| Nommage obscur | `def f(d, x):` | `def calc_tax(df, rate):` |
| Import interne | `def f(): import re` | `import re` (en haut) |
| Code dupliqué | Copier-coller | Créer une fonction |
| God function | 200 lignes | Découper en sous-fonctions |

---

## 5. Structure de projet recommandée

```
mon_projet/
├── data/
│   ├── raw/              # Données brutes (read-only)
│   └── processed/        # Données transformées
├── notebooks/
│   └── exploration.ipynb
├── src/
│   ├── __init__.py       # Expose l'API publique
│   ├── data_loader.py    # Chargement des données
│   ├── transformations.py
│   └── utils.py          # Fonctions utilitaires
├── tests/
│   └── test_transformations.py
├── config.py             # Configuration centralisée
├── requirements.txt
└── README.md
```

---

## 6. Imports et modules

```python
# Ordre des imports (PEP 8)
# 1. Bibliothèques standard
import os
import sys
from datetime import datetime

# 2. Bibliothèques tierces
import pandas as pd
import numpy as np

# 3. Modules locaux
from .utils import clean_data
from .config import SETTINGS
```

**Import relatif vs absolu :**
```python
# Relatif (dans un package)
from .utils import helper
from ..models import User

# Absolu
from myproject.utils import helper
```

---

## 7. Quand commenter ?

| ✅ Utile | ❌ Inutile |
|----------|----------|
| Expliquer le POURQUOI | Paraphraser le code |
| Avertir d'un piège/bug | `# Incrémente i` |
| TODO / FIXME temporaires | Commentaires obsolètes |
| Décisions non évidentes | Code commenté (supprimez-le) |

```python
# ✅ BON : Explique pourquoi
# Contourne bug API v2.3 qui renvoie des dates inversées
date = pd.to_datetime(date, format='%d-%m-%Y')

# ❌ MAUVAIS : Paraphrase le code
# Filtre les données actives
df_active = df[df['status'] == 'active']
```

---

## 8. Raccourcis Jupyter utiles

| Raccourci | Action |
|-----------|--------|
| `Shift + Tab` | Afficher signature/docstring |
| `Tab` | Autocomplétion |
| `Ctrl + /` | Commenter/décommenter |
| `Shift + Enter` | Exécuter cellule |
| `A` / `B` | Insérer cellule au-dessus/dessous |
| `D D` | Supprimer cellule |
| `M` | Convertir en Markdown |
| `Y` | Convertir en Code |

---

## 9. Outils de qualité de code

| Outil | Usage |
|-------|-------|
| **black** | Formatage automatique |
| **flake8** | Vérification PEP 8 |
| **isort** | Tri des imports |
| **mypy** | Vérification des types |
| **pylint** | Analyse statique |

```bash
# Installation
pip install black flake8 isort

# Usage
black mon_script.py
flake8 mon_script.py
isort mon_script.py
```

---

## 10. Ressources essentielles

- **PEP 8** : [peps.python.org/pep-0008](https://peps.python.org/pep-0008/)
- **PEP 257** (Docstrings) : [peps.python.org/pep-0257](https://peps.python.org/pep-0257/)
- **Clean Code** (livre) : Robert C. Martin
- **The Hitchhiker's Guide to Python** : [docs.python-guide.org](https://docs.python-guide.org)
- **Real Python** : [realpython.com](https://realpython.com)

---

*Module Clean Code - Master 2 Data & Strategy*
