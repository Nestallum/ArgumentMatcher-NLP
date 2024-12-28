# Projet ArgumentMatcher-NLP avec Hugging Face Hub

## Introduction
Ce projet vise à développer et comparer différents systèmes de mining d'arguments dans des textes en langage naturel, en utilisant des approches naïves, des modèles de langage large (LLM) et des techniques personnalisées.

Ce guide explique comment configurer l'environnement, installer les dépendances et utiliser la clé API Hugging Face pour s'authentifier.

---

## Prérequis
- Python 3.8 ou supérieur
- `pip` installé
- Une carte graphique NVIDIA avec CUDA (pour utiliser un GPU)

---

## Installation

### 1. Cloner le projet
Commencez par cloner ce dépôt sur votre machine locale :
```bash
git clone https://github.com/Nestallum/ArgumentMatcher-NLP.git
cd ArgumentMatcher-NLP
```

#### **Explication** :
Cette commande copie le projet depuis le dépôt GitHub vers votre ordinateur local et change le répertoire courant pour le répertoire du projet cloné.

---

### 2. Créer un environnement virtuel
Un environnement virtuel permet d'isoler les dépendances du projet. Suivez ces étapes :

1. Créez un environnement virtuel dans le répertoire du projet :
   ```bash
   python -m venv venv
   ```

2. Activez l'environnement virtuel :
   - **Windows** :
     ```bash
     .\venv\Scripts\activate
     ```
   - **Mac/Linux** :
     ```bash
     source venv/bin/activate
     ```

3. **Pour les utilisateurs souhaitant utiliser leur GPU (CUDA)** :
   Si vous souhaitez activer l'accélération GPU avec CUDA, **installez PyTorch avec la version CUDA compatible avant d'installer les autres dépendances**. 

   - **Pour CUDA 11.8** :
     ```bash
     pip install torch==2.3.1+cu118 torchvision==0.17.2+cu118 torchaudio==2.3.1+cu118 -f https://download.pytorch.org/whl/torch_stable.html
     ```

   - **Pour CUDA 11.7** :
     ```bash
     pip install torch==2.3.1+cu117 torchvision==0.17.2+cu117 torchaudio==2.3.1+cu117 -f https://download.pytorch.org/whl/torch_stable.html
     ```

4. Installez les dépendances listées dans le fichier `requirements.txt` :
   ```bash
   pip install -r requirements.txt
   ```

5. (Facultatif) Pour quitter l'environnement virtuel, utilisez :
   ```bash
   deactivate
   ```

6. (Optionnel) **Ajouter l'environnement virtuel comme kernel Jupyter**
   Si vous souhaitez exécuter les notebooks avec cet environnement virtuel, ajoutez-le comme kernel Jupyter :

   1. Installez le package `ipykernel` dans l'environnement virtuel :
      ```bash
      pip install ipykernel
      ```

   2. Ajoutez l'environnement virtuel comme kernel Jupyter :
      ```bash
      python -m ipykernel install --user --name=venv --display-name "Python (venv)"
      ```

   3. Dans Jupyter Notebook ou JupyterLab, sélectionnez le kernel **Python (venv)** pour exécuter les notebooks.

#### **Explication** :
- `venv` crée un environnement isolé pour les dépendances Python.
- L'activation permet à votre terminal d'utiliser cet environnement au lieu du Python global.
- Les dépendances spécifiques au projet sont installées via `requirements.txt`.
- L'ajout comme kernel Jupyter garantit que les notebooks utilisent le bon environnement virtuel.

---

### 3. Configuration de la clé Hugging Face

#### a) Créer un compte Hugging Face
1. Accédez à la [page de connexion](https://huggingface.co/login) et créez un compte si ce n'est pas déjà fait.
2. Une fois connecté, cliquez sur votre avatar en haut à droite, puis sur *Settings*.

#### b) Générer un **Access Token**
1. Dans *Settings*, accédez à la section *Access tokens* dans le menu de gauche.
2. Cliquez sur *New token* et créez un token de type **read**.
3. Copiez la valeur du token et conservez-la précieusement.

#### c) Stocker le token dans un fichier `.env`
Créez un fichier `.env` dans le répertoire racine du projet, et ajoutez-y la clé API comme suit :
```env
HUGGINGFACEHUB_API_TOKEN=<votre_clé>
```

> **Note :** Assurez-vous de ne jamais partager votre fichier `.env` ou votre clé en ligne.

#### **Explication** :
- La clé API Hugging Face est nécessaire pour s'authentifier et accéder aux ressources.
- Le fichier `.env` permet de stocker les variables sensibles de manière sécurisée.

---

### 4. Utilisation avec Google Colab (Optionnel)
Si vous travaillez sur Google Colab, vous pouvez créer et utiliser le fichier `.env` depuis Google Drive :

1. Montez votre Google Drive dans Colab :
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

2. Créez un fichier `.env` dans le répertoire suivant :
   ```bash
   /content/drive/MyDrive/.env
   ```

3. Ajoutez-y votre clé API Hugging Face :
   ```env
   HUGGINGFACEHUB_API_TOKEN=<votre_clé>
   ```

4. Chargez les variables d'environnement dans votre notebook :
   ```python
   from dotenv import load_dotenv
   import os

   load_dotenv('/content/drive/MyDrive/.env')
   mytoken = os.getenv('HUGGINGFACEHUB_API_TOKEN')
   print(f"Votre token est : {mytoken}")
   ```

#### **Explication** :
- Ces étapes permettent d'utiliser votre clé Hugging Face sur Colab tout en la gardant sécurisée dans Google Drive.

---

## Structure du projet
```
.
├── venv/                           # Environnement virtuel (exclu du repo Git)
├── .env                            # Clé Hugging Face (non poussé sur GitHub)
├── scripts/
│   ├── evaluate.py                 # Script pour évaluer les performances des modèles
│   ├── view_data.py                # Script pour visualiser les données
├── naive_argument_matcher.ipynb    # Notebook pour les approches naïves
├── llm_argument_matcher.ipynb      # Notebook pour les approches basées sur les LLM
├── requirements.txt                # Dépendances du projet
├── README.md                       # Documentation du projet
```
---
