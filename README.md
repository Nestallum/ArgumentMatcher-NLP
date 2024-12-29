# Projet ArgumentMatcher-NLP avec Hugging Face Hub

## Introduction
Ce projet vise à développer et comparer différents systèmes de mining d'arguments dans des textes en langage naturel, en utilisant des approches naïves, des modèles de langage large (LLM) et des techniques personnalisées.

Ce guide explique comment configurer l'environnement, installer les dépendances et utiliser la clé API Hugging Face pour s'authentifier.

---

## Prérequis
- Python 3.8 ou supérieur
- `pip` installé
- Une carte graphique NVIDIA avec CUDA (pour bénéficier de l'accélération GPU)

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
     
   - **Note** : Pour quitter l'environnement virtuel, utilisez :
      ```bash
      deactivate
      ```

3. Une fois l'environnement virtuel activé, passez à l'installation des dépendances spécifiques.

---

### 3. Préparer l'environnement pour PyTorch et accélération GPU (optionnel)

Si vous souhaitez utiliser un GPU pour entraîner ou exécuter des modèles, vous devez installer CUDA avant d'installer les packages PyTorch GPU.

1. Rendez-vous sur le site officiel de CUDA pour télécharger et installer la version appropriée pour votre GPU NVIDIA :
   [**Télécharger CUDA**](https://developer.nvidia.com/cuda-downloads)

2. Suivez les instructions pour installer CUDA et cuDNN correspondant à votre version.

3. Vérifiez que CUDA est bien installé :
   ```bash
   nvcc --version
   ```
   Cette commande doit afficher la version de CUDA installée.

4. Installez PyTorch en fonction de votre matériel :
   - **Pour les utilisateurs GPU** :
     Installez la version GPU-optimisée (CUDA 11.8) :
     ```bash
     pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
     ```

   - **Pour les utilisateurs CPU uniquement** :
     Installez la version CPU de PyTorch :
     ```bash
     pip install torch torchvision torchaudio
     ```

> **Note** : Si CUDA n'est pas installé ou si le GPU n'est pas compatible, PyTorch tombera automatiquement en mode CPU.

---

### 4. Installer les dépendances restantes
Installez les autres dépendances listées dans le fichier `requirements.txt` :
```bash
pip install -r requirements.txt
```

#### **Explication** :
- Les dépendances spécifiques au projet sont installées via `requirements.txt`.
- Assurez-vous d'avoir correctement installé PyTorch avant cette étape.

---

### 5. Configuration de la clé Hugging Face

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

### 6. Ajouter l'environnement virtuel comme kernel Jupyter (Optionnel)
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

---

### 7. Utilisation avec Google Colab (Optionnel)
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
