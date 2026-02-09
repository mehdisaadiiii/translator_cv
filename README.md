# Traducteur de CV - Dataset HSE Hackathon

Ce projet permet de traduire automatiquement un dataset de CVs et d'offres d'emploi du russe vers le français en utilisant un modèle de traduction automatique basé sur les transformers.

## 📋 Description

Le script télécharge un dataset depuis Kaggle (`darysha/hse-hackathon`), puis traduit automatiquement les colonnes textuelles pertinentes du russe vers le français en utilisant le modèle `Helsinki-NLP/opus-mt-ru-fr`.

## 🚀 Fonctionnalités

- Téléchargement automatique du dataset depuis Kaggle
- Détection automatique du délimiteur CSV
- Traduction par batch pour optimiser les performances
- Support GPU (CUDA) pour accélérer le traitement
- Traduction de 40+ colonnes incluant :
  - Informations sur les CVs (statut, localité, genre, position, compétences, etc.)
  - Informations sur les offres d'emploi (nom du poste, exigences, avantages, etc.)

## 📦 Prérequis

```bash
pip install pandas transformers torch tqdm kagglehub
```

Optionnel (recommandé pour une meilleure qualité de traduction) :
```bash
pip install sacremoses
```

## 🔧 Configuration

Les paramètres principaux peuvent être modifiés dans le notebook :

- `DATASET` : Nom du dataset Kaggle
- `FILE_PATH` : Chemin du fichier CSV dans le dataset
- `CSV_OUTPUT` : Nom du fichier de sortie
- `MODEL_NAME` : Modèle de traduction utilisé
- `BATCH_SIZE` : Taille des batches pour la traduction (défaut: 32)
- `MAX_LENGTH` : Longueur maximale des textes à traduire (défaut: 256)

## 📝 Utilisation

1. Assurez-vous d'avoir configuré vos identifiants Kaggle (voir [Kaggle API](https://www.kaggle.com/docs/api))
2. Ouvrez le notebook `traduction_cv_dataset.ipynb`
3. Exécutez toutes les cellules
4. Le fichier `train_fr.csv` sera généré avec les traductions

## 📊 Colonnes traduites

Le script traduit automatiquement les colonnes suivantes :

**Informations CV :**
- `cv_status`, `localityName`, `gender`, `positionName`
- `typicalPosition_cv`, `skills_cv`, `otherCertificates`
- `hardSkills_cv`, `softSkills_cv`, `workExperienceList`
- `scheduleType_cv`, `retrainingCapability_cv`, `languageKnowledge_cv`
- `educationList`, `relocation`, `innerInfo`, `education`

**Informations Offres d'emploi :**
- `vacancyName`, `professionalSphereName`, `vacancyAddress`
- `busyType_vacancy`, `educationRequirements`
- `hardSkills_vacancy`, `softSkills_vacancy`, `skills_vacancy`
- `typicalPosition_vacancy`, `scheduleType_vacancy`
- `otherVacancyBenefit`, `needMedcard`, `sourceType`
- `contactPerson`, `fullCompanyName`, `regionName`
- `positionRequirements`, `contactList`, `additionalRequirements`
- `qualifications`, `responsibilities`, `medicalDocument`
- `benefit`, `conditions`, `businessTrip`

Les colonnes traduites sont ajoutées avec le suffixe `_fr` (ex: `cv_status_fr`).

## 💻 Performance

- Le script utilise automatiquement le GPU si disponible (CUDA)
- Traitement par batch pour optimiser l'utilisation de la mémoire
- Barre de progression pour suivre l'avancement de chaque colonne

## 📄 Fichiers générés

- `train_fr.csv` : Dataset traduit avec les colonnes originales + colonnes traduites (`_fr`)

## 🔍 Notes

- Le script détecte automatiquement le délimiteur CSV (pipe `|` dans ce cas)
- Les valeurs nulles sont gérées automatiquement (converties en chaînes vides)
- Le modèle utilisé est spécialisé pour la traduction russe → français

## 📚 Modèle utilisé

[Helsinki-NLP/opus-mt-ru-fr](https://huggingface.co/Helsinki-NLP/opus-mt-ru-fr) : Modèle de traduction automatique russe-français basé sur OPUS-MT.

## 📝 Licence

Vérifiez la licence du dataset Kaggle utilisé avant toute utilisation commerciale.
