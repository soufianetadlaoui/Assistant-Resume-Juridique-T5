# ⚖️ Assistant de Résumé Automatique de Textes Juridiques

Ce projet propose un système de résumé automatique de textes juridiques (lois, projets de loi, rapports législatifs) utilisant le fine-tuning du modèle **T5-base** sur le dataset BillSum. 

L'objectif est de générer des résumés de qualité (ROUGE-L de 47.82%) de manière extrêmement rapide, en optimisant le temps d'entraînement et les ressources computationnelles.

## 🎯 Performances et Optimisations
Ce modèle a été optimisé pour offrir un ratio Qualité/Vitesse "Production-Ready" :
*   **Sélection Intelligente :** Entraînement ciblé sur les 8 000 meilleurs exemples du dataset au lieu des 18 949 initiaux.
*   **Vitesse :** 20 fois plus rapide qu'une approche non optimisée (T5-large), avec un temps d'entraînement réduit à 2-3 heures.
*   **Qualité :** Score ROUGE-L de 47.82% (amélioration de +55% par rapport au baseline).
*   **Robustesse :** Extraction automatique des points clés et post-processing garantissant que 100% des résumés se terminent proprement.

## 📁 Structure du Dépôt

Le projet est divisé en trois fichiers principaux :

1.  `entrainement.ipynb` : Le notebook contenant l'intégralité du pipeline de Fine-Tuning. Il inclut le chargement du dataset BillSum, la sélection intelligente des données, l'extraction des points clés, la configuration des hyperparamètres optimisés pour T5-base, et l'évaluation des métriques ROUGE.
2.  `interface.ipynb` : Le notebook contenant le code pour lancer l'interface utilisateur web interactive via **Gradio**.
3.  `modele_t5_rapide_local.zip` : L'archive contenant les poids du modèle pré-entraîné et le tokenizer nécessaires pour faire tourner l'interface sans avoir à réentraîner le modèle.

## 🚀 Installation et Utilisation

### Prérequis
Assurez-vous d'avoir Python installé ainsi que les bibliothèques suivantes :
```bash
pip install transformers gradio sentencepiece torch datasets evaluate rouge-score


Étape 1 : Préparation du modèle
Clonez ce dépôt sur votre machine locale.

https://drive.google.com/file/d/1rFuLopnfNBr376zXlM10af7643B9Vbo6/view?usp=sharing

Extrayez le contenu de l'archive modele_t5_rapide_local.zip dans le même dossier que vos notebooks. Vous devriez obtenir un dossier contenant les fichiers du modèle (ex: config.json, model.safetensors, etc.).

Étape 2 : Lancer l'Interface Gradio
Ouvrez le fichier interface.ipynb.

Assurez-vous que le chemin d'accès vers le modèle extrait (dans la cellule de chargement du modèle) pointe bien vers le dossier décompressé localement (et non vers /kaggle/input/... si vous l'exécutez en local).

Exécutez toutes les cellules du notebook.

Cliquez sur le lien local (ex: http://127.0.0.1:7860) généré par Gradio à la fin de l'exécution pour ouvrir l'interface dans votre navigateur.  

Étape 3 : Utilisation
Collez un texte juridique en anglais (minimum 50 caractères) dans la zone de texte.  

Ajustez les paramètres avancés si besoin (Longueur maximale, Beams, Pénalité de longueur).  

Cliquez sur "Générer le Résumé" pour obtenir votre résultat ainsi que les statistiques de compression.
