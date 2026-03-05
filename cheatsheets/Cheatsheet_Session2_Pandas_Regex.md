# 🐼 Cheatsheet Clean Code - Session 2
## Pandas Audit & Expressions Régulières

---

## 1. Audit initial d'un DataFrame

```python
# Vue d'ensemble
df.shape                    # (lignes, colonnes)
df.info()                   # Types, mémoire, non-null
df.describe(include='all')  # Stats descriptives
df.head(10)                 # Premières lignes
df.sample(5)                # Échantillon aléatoire
df.dtypes                   # Types par colonne
df.columns.tolist()         # Liste des colonnes
```

---

## 2. Valeurs manquantes

| Méthode | Usage |
|---------|-------|
| `df.isna()` | Masque booléen des NaN |
| `df.isna().sum()` | Compte par colonne |
| `df.isna().sum().sum()` | Total de NaN |
| `df.dropna()` | Supprime lignes avec NaN |
| `df.dropna(subset=['col'])` | Supprime si NaN dans col |
| `df.fillna(value)` | Remplace NaN par value |
| `df.fillna(df.mean())` | Imputation par moyenne |
| `df.fillna(method='ffill')` | Forward fill |
| `df.interpolate()` | Interpolation |

**Rapport de valeurs manquantes :**
```python
missing = pd.DataFrame({
    'count': df.isna().sum(),
    'pct': (df.isna().sum() / len(df) * 100).round(2)
}).sort_values('pct', ascending=False)
```

**Fausses valeurs nulles :**
```python
false_nulls = ['', 'N/A', 'n/a', 'NA', 'null', 'None', '-']
df.replace(false_nulls, np.nan, inplace=True)
```

---

## 3. Doublons

```python
df.duplicated()                        # Masque booléen
df.duplicated().sum()                  # Nombre de doublons
df.duplicated(subset=['col1', 'col2']) # Sur colonnes spécifiques
df.duplicated(keep='first')            # Garde le premier
df.duplicated(keep='last')             # Garde le dernier
df.duplicated(keep=False)              # Marque TOUS les doublons
df.drop_duplicates()                   # Supprime les doublons
```

---

## 4. Sélection et filtrage

### .loc[] - Label-based
```python
df.loc[condition, 'column']
df.loc[df['age'] > 30, 'name']
df.loc[df['city'].isin(['Paris', 'Lyon']), ['name', 'age']]
df.loc[(df['a'] > 0) & (df['b'] < 10), :]
```

### .iloc[] - Index-based
```python
df.iloc[0:10, 2:5]      # Lignes 0-9, colonnes 2-4
df.iloc[[0, 5, 10], :]  # Lignes spécifiques
df.iloc[:, [0, -1]]     # Première et dernière colonne
```

### .query() - SQL-like
```python
df.query("age > 30")
df.query("city == 'Paris' and age > 25")
df.query("category in ['A', 'B']")
df.query("amount > @min_value")  # Variable externe
```

### Masques booléens
```python
mask = (df['a'] > 0) & (df['b'] < 10) | (df['c'] == 'X')
df[mask]
```

---

## 5. Expressions régulières essentielles

| Pattern | Description | Exemple |
|---------|-------------|---------|
| `\d` | Chiffre | `0-9` |
| `\d+` | Un ou plusieurs chiffres | `123`, `45` |
| `\d{5}` | Exactement 5 chiffres | `75001` |
| `\w` | Alphanumérique + _ | `a-z`, `0-9`, `_` |
| `\s` | Espace, tab, newline | ` `, `\t`, `\n` |
| `\S` | Non-espace | |
| `[A-Z]` | Majuscule | `A-Z` |
| `[a-z]` | Minuscule | `a-z` |
| `[^abc]` | Tout sauf a, b, c | |
| `^` | Début de chaîne | `^Hello` |
| `$` | Fin de chaîne | `.com$` |
| `(a|b)` | a OU b | `(oui|non)` |
| `.*` | N'importe quoi | |
| `.+` | Au moins 1 caractère | |
| `?` | 0 ou 1 occurrence | `colou?r` |

**Patterns utiles :**
```python
# Email
r'^[\w.-]+@[\w.-]+\.[a-zA-Z]{2,}$'

# Téléphone français (10 chiffres)
r'^0[1-9]\d{8}$'

# Code postal français
r'^\d{5}$'

# Date YYYY-MM-DD
r'^\d{4}-\d{2}-\d{2}$'

# URL
r'https?://[\w.-]+\.[a-zA-Z]{2,}.*'
```

---

## 6. Méthodes str de Pandas

| Méthode | Usage | Exemple |
|---------|-------|---------|
| `.str.contains()` | Contient pattern | `df[df['col'].str.contains('abc')]` |
| `.str.match()` | Commence par pattern | `df['col'].str.match(r'^\d+')` |
| `.str.extract()` | Extraire groupe | `df['col'].str.extract(r'(\d+)')` |
| `.str.replace()` | Remplacer | `df['col'].str.replace(r'\D', '', regex=True)` |
| `.str.split()` | Découper | `df['col'].str.split(',')` |
| `.str.lower()` | Minuscules | |
| `.str.upper()` | Majuscules | |
| `.str.strip()` | Suppr espaces | |
| `.str.len()` | Longueur | |
| `.str.startswith()` | Commence par | |
| `.str.endswith()` | Finit par | |

**Exemples pratiques :**
```python
# Nettoyer téléphone (garder chiffres)
df['phone_clean'] = df['phone'].str.replace(r'\D', '', regex=True)

# Extraire domaine email
df['domain'] = df['email'].str.extract(r'@([\w.-]+)')

# Valider format
df['email_valid'] = df['email'].str.match(r'^[\w.-]+@[\w.-]+\.\w+$')

# Filtrer lignes
df[df['text'].str.contains('mot', case=False, na=False)]
```

---

## 7. Agrégations et statistiques

### Méthodes descriptives
```python
df['col'].mean()          # Moyenne
df['col'].median()        # Médiane
df['col'].std()           # Écart-type
df['col'].min() / .max()  # Min / Max
df['col'].sum()           # Somme
df['col'].count()         # Compte (non-null)
df['col'].nunique()       # Valeurs uniques
df['col'].value_counts()  # Fréquences
df['col'].quantile([.25, .5, .75])  # Quantiles
```

### GroupBy et agrégations
```python
# Simple
df.groupby('category')['amount'].sum()

# Multiple
df.groupby('category').agg({
    'amount': ['sum', 'mean', 'count'],
    'quantity': 'sum'
})

# Avec lambda
df.groupby('cat').agg({
    'val': lambda x: x.quantile(0.9)
})

# Renommer
df.groupby('cat')['amount'].sum().reset_index(name='total')
```

### Pivot tables
```python
pd.pivot_table(
    df,
    values='amount',
    index='category',
    columns='channel',
    aggfunc='mean',
    fill_value=0
)
```

---

## 8. Chaînage de méthodes

```python
result = (
    df
    .query("amount > 0")
    .assign(
        amount_ttc=lambda x: x['amount'] * 1.2,
        category_upper=lambda x: x['category'].str.upper()
    )
    .groupby('category_upper')
    .agg({'amount_ttc': ['sum', 'mean']})
    .sort_values(('amount_ttc', 'sum'), ascending=False)
    .round(2)
)
```

---

## 9. Formatage et export

### Styler Pandas
```python
(df
 .style
 .background_gradient(cmap='RdYlGn', subset=['amount'])
 .format({'amount': '{:,.2f}€', 'pct': '{:.1%}'})
 .highlight_max(color='lightgreen')
 .highlight_min(color='lightcoral')
)
```

### Export
```python
# CSV
df.to_csv('output.csv', index=False, encoding='utf-8')

# Excel
df.to_excel('output.xlsx', index=False, sheet_name='Data')

# Excel multi-onglets
with pd.ExcelWriter('report.xlsx') as writer:
    df1.to_excel(writer, sheet_name='Summary')
    df2.to_excel(writer, sheet_name='Details')
```

---

## 10. Ressources

- **Pandas** : [pandas.pydata.org/docs](https://pandas.pydata.org/docs)
- **Regex101** : [regex101.com](https://regex101.com) (testeur interactif)
- **Pandas Cheatsheet** : [pandas.pydata.org/Pandas_Cheat_Sheet.pdf](https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf)
- **Real Python Pandas** : [realpython.com/pandas-python-explore-dataset](https://realpython.com/pandas-python-explore-dataset/)

---

*Module Clean Code - Master 2 Data & Strategy*
