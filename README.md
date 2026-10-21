# TP4 : Système RAG sur mon CV

**Étudiante :** Jihane Salek, Master Intelligence Artificielle et Digital Computing (FST Béni Mellal)

Implémentation d'un système **RAG** (Retrieval-Augmented Generation) sur mon CV, avec évaluation de la fidélité des réponses par un LLM-juge.

## Contenu du dépôt

| Fichier / dossier | Description |
|---|---|
| `rag.ipynb` | Notebook Python (code + résultats d'exécution) |
| `Reponses_TP3_RAG.docx` | Document de réponses avec captures d'écran |
| `screens/` | Captures d'écran prouvant la réalisation des tâches |
| `pdfs/cv.pdf` | Document utilisé (mon CV) |
| `rag_juge.gif` | Schéma de l'architecture d'évaluation |

## Pipeline réalisé

1. Chargement du PDF (`PyPDFLoader`)
2. Découpage en chunks (300 tokens, overlap 20)
3. Embeddings (`gemini-embedding-001`) et stockage dans ChromaDB
4. Retriever (similarité, k = 5)
5. Prompt avec règle anti-hallucination (« Je ne sais pas ! »)
6. Génération avec `gemini-3.1-flash-lite`
7. Évaluation de la groundedness par un LLM-juge (`gemini-3-flash-preview`)

## Résultats

- 1 page, 5 chunks, 5 chunks indexés, 5 chunks récupérés
- Score du juge : 5/5 sur les 4 questions (dont une question hors contexte, qui donne « Je ne sais pas ! »)

## Exécuter le projet

1. Installer les dépendances avec uv :
   `uv add ipykernel langchain langchain-text-splitters langchain-community pypdf tiktoken chromadb langchain-chroma python-dotenv pandas langchain-google-genai`
2. Créer un fichier `.env` à la racine avec : `GOOGLE_API_KEY=votre_cle`
3. Ouvrir `rag.ipynb` et exécuter les cellules de haut en bas.

> Le fichier `.env` (clé API) n'est pas publié sur GitHub.
