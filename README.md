---
title: Assistant RAG IA
emoji: 🤖
colorFrom: blue
colorTo: purple
sdk: streamlit
app_file: src/streamlit_app.py
pinned: false
---

# Agent RAG — Assistant sur l'Intelligence Artificielle

Un assistant qui répond à mes questions sur l'IA en s'appuyant uniquement sur mes propres documents PDF.

---

## C'est quoi le RAG ?

**RAG = Retrieval-Augmented Generation** (génération augmentée par la récupération)

Au lieu de laisser le modèle répondre de mémoire, mon système :
1. **Cherche** les passages les plus pertinents dans mes documents
2. **Donne** ces passages au modèle avec ma question
3. Le modèle **répond uniquement** à partir de ce contexte — pas d'invention

Les réponses sont plus fiables et je sais toujours d'où elles viennent.

---

## Structure du projet

```
agent_rag/
├── documents/          ← Mes PDFs (IA, machine learning, deep learning)
├── faiss_index/        ← Base vectorielle générée par le notebook
├── rag.ipynb           ← Notebook : construction de l'index + tests
├── streamlit_app.py    ← Interface web interactive
├── requirements.txt    ← Toutes les dépendances Python
└── .env                ← Ma clé API Google (à créer, ne jamais committer !)
```

---

## Installation

### 1. Créer un environnement virtuel

```bash
python -m venv .venv
source .venv/bin/activate      # Windows : .venv\Scripts\activate
```

### 2. Installer les dépendances

```bash
pip install -r requirements.txt
```

### 3. Créer le fichier `.env`

```
GOOGLE_API_KEY=ma_cle_api_ici
```

> Je génère ma clé gratuitement sur [aistudio.google.com/app/apikey](https://aistudio.google.com/app/apikey)

---

## Utilisation

### Étape 1 — Construire la base vectorielle (une seule fois)

J'ouvre `rag.ipynb` et j'exécute toutes les cellules dans l'ordre.
Cela crée le dossier `faiss_index/` sur mon disque.

> Je n'ai besoin de refaire cette étape que si j'ajoute de nouveaux documents.

### Étape 2 — Lancer l'interface

```bash
streamlit run src/streamlit_app.py
```

L'application s'ouvre dans mon navigateur, je pose ma question et j'obtiens une réponse avec les sources.

---

## Technologies utilisées

| Outil | Rôle |
|---|---|
| LangChain | Orchestre tout le pipeline RAG |
| FAISS | Stocke les vecteurs et fait la recherche sémantique |
| FastEmbedEmbeddings | Calcule les embeddings en local (gratuit, sans quota) |
| Gemini (Google) | Génère les réponses à partir du contexte |
| Streamlit | Interface web |

---

## Problèmes fréquents

**`faiss_index` introuvable** → Exécuter d'abord toutes les cellules du notebook.

**Erreur 429 quota dépassé** → Créer une nouvelle clé API sur Google AI Studio.

**Réponse "je n'ai pas les informations"** → La réponse n'est pas dans les PDFs fournis.# 