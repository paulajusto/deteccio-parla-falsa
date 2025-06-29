# Detecció de Parla Falsa amb Aprenentatge Automàtic

Aquest projecte implementa un sistema de classificació per distingir entre àudios reals i àudios generats mitjançant tècniques d’intel·ligència artificial. Inclou un procés complet de preparació de dades, entrenament de models i anàlisi de resultats.

## Objectius

- Preparar i analitzar un conjunt de dades amb més de 80.000 mostres d’àudio.
- Entrenar models predictius capaços d’identificar patrons per classificar els àudios.
- Comparar diversos algoritmes supervisats i seleccionar el millor model segons criteris objectius de rendiment.
- Documentar tot el procés amb un Model Card que descrigui les característiques, limitacions i recomanacions d’ús del model.

## Conjunt de dades

El dataset inclou característiques acústiques i metadades com:

- MFCCs, loudness, jitter i altres variables numèriques.
- Informació de sexe i país dels enregistraments.
- Etiquetes binàries que indiquen si l’àudio és real o sintètic.

Les dades s’han preprocessat mitjançant:

- Imputació de valors nuls amb la mediana.
- Eliminació d’outliers amb l’IQR.
- Recodificació i One-Hot-Encoding de variables categòriques.
- Normalització logarítmica i StandardScaler en funció de la distribució de cada variable.

## Models Implementats

S’han desenvolupat i comparat tres models principals:

- **KNN**  
  Entrenat amb i sense reducció dimensional amb PCA. Sense PCA ha aconseguit una AUC-ROC de 0.87 i una precisió superior.
- **Arbre de Decisió**  
  Amb una AUC-ROC de 0.84 sense PCA i una interpretabilitat elevada.
- **SVM**  
  El model amb millor rendiment global, especialment sense PCA, assolint una AUC-ROC de 0.90 i una accuracy de 83%.

També s’ha entrenat un **Explainable Boosting Machine (EBM)** amb una capacitat predictiva competitiva i una alta interpretabilitat.

## Resultats Principals

| Model              | Accuracy (Test) | AUC-ROC |
|--------------------|-----------------|---------|
| KNN                | 78%             | 0.87    |
| Arbre de Decisió   | 77%             | 0.84    |
| SVM                | 83%             | 0.90    |
| EBM                | 82%             | 0.90    |

L’ús de totes les variables originals sense PCA ha demostrat un augment substancial del rendiment respecte a la reducció dimensional.

## Model Seleccionat

El model final seleccionat és un SVM amb kernel radial (RBF) i C=10, entrenat sense reducció dimensional. Aquest model combina una alta capacitat de discriminació amb una robustesa consistent en validació i test.

## Mètriques del Model Final

- Accuracy test final: 80%
- AUC-ROC test final: 0.80

## Limitacions i Recomanacions

- El model pot veure’s afectat per àudios de baixa qualitat o dominis geogràfics no representats.
- És necessari aplicar el mateix pipeline de preprocessament per garantir la consistència dels resultats.
- Es recomana reentrenar periòdicament el model amb dades actualitzades.

## Tecnologia i Llibreries

- Python
- scikit-learn
- pandas, NumPy
- OpenSMILE per a l’extracció de característiques acústiques

## Reproducció dels Experiments

1. Preprocessar els conjunts de dades aplicant el mateix procediment utilitzat en l’entrenament.
2. Entrenar els models amb els scripts corresponents.
3. Validar i avaluar els models amb els conjunts de test.
4. Revisar les mètriques i les corbes ROC per comparar el rendiment.

## Referències

- [scikit-learn](https://scikit-learn.org)
- [OpenSMILE](https://audeering.github.io/opensmile)

## Llicència

Aquest projecte s’ha desenvolupat amb finalitats acadèmiques. L’ús en entorns productius requereix una validació addicional i proves de robustesa.
