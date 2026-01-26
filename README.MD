# GeneFusion BWT: Feature Extraction e Classificazione su Dati Genomici Reali

## 🧬 Descrizione del Problema
Le **fusioni geniche** sono anomalie in cui parti di due o più geni originari si uniscono per formare un gene "ibrido". Questi eventi non sono casuali, ma agiscono come *driver molecolari* capaci di innescare la trasformazione maligna e sostenere la progressione tumorale.

Poiché le fusioni somatiche si trovano esclusivamente nelle cellule cancerose, rappresentano target ideali per:
* **Precisione Diagnostica:** Conferma di sottotipi specifici di cancro (es. BCR-ABL1).
* **Target Terapeutico:** Progettazione di farmaci che colpiscono selettivamente le cellule malate.
La sfida computazionale risiede nel distinguere i veri driver biologici dagli **artefatti tecnici** (rumore di fondo) generati durante il processo di sequenziamento.

## 🔬 Analisi del Problema e Metodologia
Lo studio propone una pipeline di analisi che trasforma sequenze genomiche grezze in vettori di feature numeriche, utilizzando tecniche avanzate di elaborazione stringhe e Machine Learning.

### Dataset e Preprocessing
* **Dati:** Dataset reale bilanciato (Non-Fusion: ~148k, Fusion: ~116k).
* **Preprocessing:** Rimozione duplicati e segmentazione delle sequenze tramite *windowing dinamico* a 1000 nucleotidi
* **Gestione Sbilanciamento:** Stratificazione (80/20 split) e Class Weighting durante il training.

### Feature Engineering
L'approccio innovativo risiede nell'estrazione di feature strutturali tramite la **Burrows-Wheeler Transform (BWT)**, confrontata con metriche bio-linguistiche:
1.  **Statistiche di Base:** GC Content, Entropia di Shannon su sequenza originale.
2.  **Caratteristiche Strutturali BWT:** BWT Entropy, Run Length Analysis, Compression Ratio. Sono state testate tre varianti: *Classica, Positional, Reverse-Complement*.
3.  **Analisi Bio-Linguistica:** KL Divergence (Kullback-Leibler) e densità dei Codoni di Stop.

### Modelli Utilizzati
Sono stati addestrati tre algoritmi di classificazione:
* **Random Forest (RF)**
* **XGBoost (XGB)**
* **Multilayer Perceptron (MLP - Rete Neurale)**

## 🎯 Obiettivo dello Studio 
L'obiettivo principale è validare se la riorganizzazione delle informazioni tramite BWT possa far emergere pattern strutturali invisibili nelle letture grezze (reads), migliorando la classificazione automatica.
