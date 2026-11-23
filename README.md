# 🩺 Chatbot-Médical-Intelligent

Chatbot médical intelligent et **multimodal** reposant sur une architecture **RAG (Retrieval-Augmented Generation)**. Il répond aux questions de santé à partir d'une source de référence, *The Gale Encyclopedia of Medicine (Second Edition)*, et complète ses réponses par une **recherche web via Tavily** lorsque le document est incomplet ou que l'information est potentiellement obsolète.

## 1. ✨ Fonctionnalités

- **Entrées multimodales**
  - 💬 **Texte** : questions en langage naturel
  - 🖼️ **Images** : analyse d'images (ex. lésion cutanée, ordonnance, notice de médicament)
  - 🎥 **Vidéos** : analyse de séquences vidéo importées
  - 📷 **Caméra en direct** : capture et analyse en temps réel
- **RAG sur document de référence** : récupération sémantique des passages pertinents de The Gale Encyclopedia of Medicine, 2nd Edition.
- **Recherche web via Tavily** : activée automatiquement si la couverture documentaire est insuffisante ou si l'information doit être mise à jour (traitements récents, nouvelles recommandations).
- **Lecture vocale des réponses** 🔊 : synthèse vocale (text-to-speech) pour écouter les réponses du chatbot, utile pour l'accessibilité.
- **Réponses sourcées** : distinction claire entre les informations issues de l'encyclopédie et celles issues du web.

## 2. 🧠 Fonctionnement

1. L'utilisateur envoie une entrée (texte, image, vidéo ou flux caméra).
2. Les contenus visuels sont analysés par un modèle multimodal pour en extraire une description exploitable.
3. Les passages pertinents sont récupérés dans la base vectorielle issue de l'encyclopédie.
4. Si la couverture est insuffisante ou l'information semble ancienne, une recherche Tavily est déclenchée.
5. Le LLM génère une réponse à partir du contexte combiné (document + web).
6. La réponse est affichée et peut être lue à voix haute.

## 3. 📁 Structure du projet

```
├── app/
│   ├── config.py        # Variables d'environnement + contournement SSL (Conda)
│   ├── knowledge.py     # Récupération vectorielle Pinecone
│   ├── agent.py         # Graphe LangGraph : retrieve → route → Tavily → answer
│   └── main.py          # API FastAPI : observations d'images, endpoints Whisper et TTS
├── data/
│   └── medical_book.pdf # PDF de référence (fourni par l'utilisateur)
├── static/
│   ├── style.css        # Styles
│   └── app.js           # Contrôles côté navigateur
├── templates/
│   └── index.html       # Interface utilisateur
└── ingest.py            # Découpage et vectorisation de chaque page lisible du PDF
```

## 4. 🚀 Exécuter le projet
  1. Cloner le dépôt
bash `git clone https://github.com/<votre-compte>/Chatbot-Médical-Intelligent.git`
`cd Chatbot-Médical-Intelligent`
  2. Installer uv (si nécessaire)

Vérifiez d'abord s'il est déjà installé : bash `uv --version`

Sinon, installez-le selon votre système :

Système	Commande
Windows	powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex" ou winget install --id=astral-sh.uv -e
Linux / macOS	curl -LsSf https://astral.sh/uv/install.sh | sh
macOS (Homebrew)	brew install uv
Tous (via pip)	pip install uv

Fermez puis rouvrez le terminal, et revérifiez avec uv --version.

Pour mettre à jour uv plus tard : uv self update (ou pip install -U uv si installé avec pip).

  3. Configurer les variables d'environnement
bash
cp .env.example .env          # Windows (PowerShell) : copy .env.example .env

Ouvrez .env et renseignez vos clés (Pinecone, Tavily, fournisseur LLM, etc.).

  4. Installer les dépendances bash uv sync (Cette commande crée automatiquement l'environnement virtuel .venv s'il n'existe pas, puis installe les dépendances du projet.)

  5. Indexer le document de référence

Placez votre PDF dans data/medical_book.pdf, puis lancez l'indexation (une seule fois, ou après chaque changement de document) : 
bash uv run python ingest.py
  6. Lancer l'application bash uv run uvicorn app.main:app --reload

L'interface est disponible sur http://127.0.0.1:8000.

## ⚠️ Avertissement

Ce projet est fourni à des fins **informatives et éducatives uniquement**. L'analyse d'images et de vidéos ne constitue **pas un diagnostic médical** et ne remplace en aucun cas l'avis d'un professionnel de santé qualifié. Pour toute urgence médicale, contactez immédiatement les services d'urgence.

## 🛠️ Stack technique

RAG · Modèle multimodal (vision) · Tavily API · Text-to-Speech · Base vectorielle · Python
