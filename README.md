# ArgumentMatcher-NLP
This project aims to develop and compare multiple argument mining systems in natural language texts, using naive approaches, large language models (LLM)-based methods, and custom techniques.

# Projet Python avec Hugging Face Hub

## Introduction
Ce projet utilise Hugging Face Hub pour accéder à des modèles et jeux de données d'IA. Ce guide explique comment configurer l'environnement, installer les dépendances et utiliser la clé API Hugging Face pour s'authentifier.

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
git clone https://github.com/ton-utilisateur/ton-repo.git
cd ton-repo
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

3. Installez les dépendances listées dans le fichier `requirements.txt` :
   ```bash
   pip install -r requirements.txt
   ```

4. (Facultatif) Pour quitter l'environnement virtuel, utilisez :
   ```bash
   deactivate
   ```

#### **Explication** :
- `venv` crée un environnement isolé pour les dépendances Python.
- L'activation permet à votre terminal d'utiliser cet environnement au lieu du Python global.
- Les dépendances spécifiques au projet sont installées via `requirements.txt`.

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

### 4. Configuration pour utiliser le GPU (optionnel)
Si vous souhaitez utiliser un GPU pour entraîner ou exécuter des modèles, suivez les étapes ci-dessous :

1. Assurez-vous d'avoir une carte graphique NVIDIA et que les pilotes CUDA sont installés.
   - Téléchargez et installez les [pilotes CUDA](https://developer.nvidia.com/cuda-downloads).
   - Installez également [cuDNN](https://developer.nvidia.com/cudnn).

2. Vérifiez que PyTorch est compatible avec CUDA :
   ```bash
   pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
   ```
   - Remplacez `cu118` par la version CUDA installée sur votre machine (par exemple `cu117` pour CUDA 11.7).

3. Testez la disponibilité du GPU dans votre environnement :
   ```python
   import torch

   print("PyTorch version:", torch.__version__)
   print("CUDA available:", torch.cuda.is_available())
   if torch.cuda.is_available():
       print("GPU:", torch.cuda.get_device_name(0))
   else:
       print("Aucun GPU détecté ou CUDA n'est pas installé.")
   ```

#### **Explication** :
- Ces étapes permettent de configurer et de vérifier l'accès au GPU pour accélérer les calculs.
- PyTorch est la bibliothèque utilisée pour exploiter le GPU via CUDA.

---

### 5. Utilisation avec Google Colab (Optionnel)
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
├── venv/                  # Environnement virtuel (exclu du repo Git)
├── .env                   # Clé Hugging Face (non poussé sur GitHub)
├── requirements.txt       # Dépendances du projet
├── main.py                # Fichier principal du projet
├── README.md              # Documentation du projet
```

#### **Explication** :
- `venv/` contient l'environnement virtuel et doit être exclus avec `.gitignore`.
- `.env` contient les variables sensibles comme les clés API.
- `requirements.txt` liste les dépendances du projet pour une installation facile.

---

## Contribuer
Les contributions sont les bienvenues ! Merci de :
- Créer une branche pour vos modifications.
- Documenter vos changements avant de soumettre une pull request.

---

## Licence
Ce projet est sous licence MIT. Consultez le fichier [LICENSE](LICENSE) pour plus de détails.
