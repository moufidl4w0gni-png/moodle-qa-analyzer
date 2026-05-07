# 📚 Analyseur de questions Moodle QA

Application Streamlit pour analyser, détecter les erreurs et corriger automatiquement le barème des questions Moodle.

## 🚀 Démo en ligne

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io)

---

## ✨ Fonctionnalités

| Fonctionnalité | Description |
|---|---|
| 📥 Import XML & GIFT | Support des deux formats d'export Moodle |
| 🔍 Détection HTML/LaTeX | Balises déséquilibrées, LaTeX non fermé |
| 🖼️ Graphiques manquants | Détecte les références visuelles sans image |
| 📝 Cohérence réponses | Doublons, vide, bonne réponse manquante |
| 🔤 Encodage | Détecte les caractères mal encodés (UTF-8) |
| 🔧 Correction barème | Ajuste automatiquement fractions et pénalités |
| 📊 Export Excel | Rapport multi-feuilles (analyse + corrections) |
| 📄 Export XML corrigé | Fichier prêt à réimporter dans Moodle |
| 🤖 Vérification IA | Vérifie la pertinence des réponses via Claude |

---

## 📦 Installation locale

```bash
# 1. Cloner le dépôt
git clone https://github.com/VOTRE_NOM/moodle-qa-analyzer.git
cd moodle-qa-analyzer

# 2. Créer un environnement virtuel (recommandé)
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows

# 3. Installer les dépendances
pip install -r requirements.txt

# 4. Lancer l'application
streamlit run app.py
```

L'application s'ouvre automatiquement sur `http://localhost:8501`

---

## ☁️ Déploiement sur Streamlit Cloud (gratuit)

### Étape 1 — Préparer le dépôt GitHub

1. Créez un compte sur [github.com](https://github.com) si ce n'est pas fait
2. Créez un **nouveau dépôt public** (ex: `moodle-qa-analyzer`)
3. Uploadez tous les fichiers de ce projet :
   - `app.py`
   - `requirements.txt`
   - `README.md`
   - `.streamlit/config.toml`

### Étape 2 — Déployer sur Streamlit Cloud

1. Allez sur [share.streamlit.io](https://share.streamlit.io)
2. Connectez-vous avec votre compte GitHub
3. Cliquez **"New app"**
4. Sélectionnez votre dépôt et le fichier `app.py`
5. Cliquez **"Deploy"** — l'app est en ligne en 2 minutes !

### Étape 3 — Configurer la clé API (optionnel)

Pour activer la vérification IA :

1. Dans Streamlit Cloud, allez dans **Settings → Secrets**
2. Ajoutez :
```toml
ANTHROPIC_API_KEY = "sk-ant-votre-clé-ici"
```

---

## 📁 Structure du projet

```
moodle-qa-analyzer/
├── app.py                  # Application principale Streamlit
├── requirements.txt        # Dépendances Python
├── README.md               # Ce fichier
└── .streamlit/
    └── config.toml         # Configuration Streamlit
```

---

## 🔧 Correction automatique du barème

L'application corrige automatiquement :

| Problème | Correction |
|---|---|
| Bonne réponse ≠ 100% | → mise à 100% |
| Mauvaise réponse > 0% | → mise à 0% |
| Fraction > 100% ou < −100% | → ramenée aux limites |
| Pénalité non standard | → ajustée (défaut : 1/3) |

**Pénalités disponibles :** 0, 1/10, 1/3, 1/2, 1

---

## 🐛 Problèmes détectés

### HTML / LaTeX
- Balises ouvertes non fermées (heuristique avancée)
- LaTeX `$$` en nombre impair
- LaTeX `\( \)` ou `\[ \]` déséquilibré
- Entités HTML invalides (`&` sans `;`)
- `<img>` sans attribut `src`

### Graphiques
- Référence à "graphique", "figure", "ci-dessous"... sans `<img>`

### Réponses
- Aucune bonne réponse définie
- Réponses dupliquées
- Réponses vides
- Moins de 2 réponses (multichoice)

### Encodage
- Caractères UTF-8 mal encodés (é → Ã©, etc.)
- Guillemets et apostrophes malformés

---

## 📄 Licence

MIT — libre d'utilisation et de modification.
