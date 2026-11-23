# Chatbot-Medical-Intelligent
Chatbot médical multimodal basé sur un système RAG (The Gale Encyclopedia of Medicine, 2e éd.) avec recherche web Tavily. Accepte texte, images, vidéos et caméra en direct, avec lecture vocale des réponses.


# 🩺 Chatbot-Médical-Intelligent

Chatbot médical intelligent et **multimodal** reposant sur une architecture **RAG (Retrieval-Augmented Generation)**. Il répond aux questions de santé à partir d'une source de référence, *The Gale Encyclopedia of Medicine (Second Edition)*, et complète ses réponses par une **recherche web via Tavily** lorsque le document est incomplet ou que l'information est potentiellement obsolète.

## ✨ Fonctionnalités

- **Entrées multimodales**
  - 💬 **Texte** : questions en langage naturel
  - 🖼️ **Images** : analyse d'images (ex. lésion cutanée, ordonnance, notice de médicament)
  - 🎥 **Vidéos** : analyse de séquences vidéo importées
  - 📷 **Caméra en direct** : capture et analyse en temps réel
- **RAG sur document de référence** : récupération sémantique des passages pertinents de The Gale Encyclopedia of Medicine, 2nd Edition.
- **Recherche web via Tavily** : activée automatiquement si la couverture documentaire est insuffisante ou si l'information doit être mise à jour (traitements récents, nouvelles recommandations).
- **Lecture vocale des réponses** 🔊 : synthèse vocale (text-to-speech) pour écouter les réponses du chatbot, utile pour l'accessibilité.
- **Réponses sourcées** : distinction claire entre les informations issues de l'encyclopédie et celles issues du web.

## 🧠 Fonctionnement

1. L'utilisateur envoie une entrée (texte, image, vidéo ou flux caméra).
2. Les contenus visuels sont analysés par un modèle multimodal pour en extraire une description exploitable.
3. Les passages pertinents sont récupérés dans la base vectorielle issue de l'encyclopédie.
4. Si la couverture est insuffisante ou l'information semble ancienne, une recherche Tavily est déclenchée.
5. Le LLM génère une réponse à partir du contexte combiné (document + web).
6. La réponse est affichée et peut être lue à voix haute.

## ⚠️ Avertissement

Ce projet est fourni à des fins **informatives et éducatives uniquement**. L'analyse d'images et de vidéos ne constitue **pas un diagnostic médical** et ne remplace en aucun cas l'avis d'un professionnel de santé qualifié. Pour toute urgence médicale, contactez immédiatement les services d'urgence.

## 🛠️ Stack technique

RAG · Modèle multimodal (vision) · Tavily API · Text-to-Speech · Base vectorielle · Python
