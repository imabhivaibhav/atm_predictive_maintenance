# ATM Predictive Maintenance Using Random Forest and XGBoost

## Project Title
Predictive Maintenance of ATM Utilizing Multi-Label and Binary Fault Classification Through Random Forest and XGBoost

## Author
Abhijeet Vaibhav

***

## Abstract
The project ensures continuous and reliable functionality of Automated Teller Machines (ATMs), which is crucial for banking operations. It compares two tree-based machine learning classifiers, Random Forest and XGBoost, for forecasting ATM fault occurrences. The classification includes multi-label detection of fault types and binary detection of fault presence. Evaluation metrics such as precision, recall, F1-score, and confusion matrices analyze their performance on real-world ATM datasets.

***

## Introduction
Unscheduled ATM downtime due to faults causes customer inconvenience and financial loss. Predictive maintenance strategies aim to identify these faults in advance using data-driven methods. This study applies Random Forest and XGBoost for both multi-label and binary classification to forecast faults, providing detailed diagnostics and enabling proactive maintenance interventions.

***

## Dataset and Preprocessing

- **Data Sources:** Transaction logs, metadata, site characteristics, and historical maintenance records spanning May to October 2021.
- **Features:** Categorical (ATM model, region, site type) and numerical (daily transactions, maintenance durations).
- **Encoding:** Ordinal encoding for categorical features.
- **Temporal Split:** May-September 2021 used for training; September-October 2021 for testing.

### Unique Fault Types after combining similar fualts

-Card Reader Failure
-Cash Handler Fault
-Cashout Fault
-Cassette Fault
-Close
-Communication Failure
-Depository Fault
-Encryptor Fault
-Power Failure
-Receipt Printer Fault
-Supervisor Switch On
-Suspected Skimming Attack


  
Fig 2: Merged fault categories.

### Site Category Fault Counts



| Original Site Category              | Count   | Merged Site Category        | Count   |
|-----------------------------------|---------|-----------------------------|---------|
| Site not under special category   | 499,514 | Site not under special category | 499,667 |
| Other                             | 31,059  | Other                      | 32,589  |
| E-LOBBY                          | 20,890  | E-LOBBY                   | 19,890  |
| Lobby ATM                       | 14,535  | Lobby ATM                | 14,535  |
| ...                             | ...     | ...                        | ...     |


![ATM avg monthly count.jpg]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/ATM_avg_monthly_count.jpg))

Fig 1: Count of ATM and there Monthly avg faults.

![Monthly fault count.jpg]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/Monthly_Fault_count.jpg))

Fig 2: Monthly fault count.

Faults with maintenance not done include:
- Cashout Fault
- Power Failure
- Suspected Skimming Attack

***

## Methodology

### 1. Multi-Label Classification

| **Features**               | **Target**                      |
|-----------------------------|----------------------------------|
| ATM ID                      | Card Reader Failure             |
| atm_type                    | Cash Handler Fault              |
| Machine type                | Cashout Fault                   |
| Site type                   | Cassette Fault                  |
| Region                      | Close                           |
| Zone                        | Communication Failure           |
| Site Category               | Depository Fault                |
| ATM_Hits                    | Encryptor Fault                 |
| rolling_hits_7d              | Power Failure                   |
| Duration                    | Receipt Printer Fault           |
| Maintenance in last 7d      | Supervisor Switch On            |
| Maintenance Duration        | Suspected Skimming Attack       |

- Uses multi-output classifiers (Random Forest and XGBoost).
- Predicts multiple concurrent fault types per ATM.
- Features include ATM ID, model, type, region, transaction counts, and maintenance history.
- Targets are 12 fault categories (as listed above).

### 2. Binary Classification
- Predicts presence or absence of any fault.
- Uses aggregated fault labels or direct binary classifier.
- Similar features but binary target of fault/no-fault.


| **Features**                | **Target*       |
|-----------------------------|-----------------|
| ATM ID                      | Fault           |
| atm_type                    |                 |
| Machine type                |                 |
| Site type                   |                 |
| Region                      |                 |
| Zone                        |                 |
| Site Category               |                 |
| ATM_Hits                    |                 |
| rolling_hits_7d             |                 |
| Duration                    |                 |



### Sliding Window Fault Prediction
- Observation window: 14 days of historical data.
- Buffer window: 7-day gap to prevent data leakage.
- Prediction window: Next 10 days for fault forecasting.
- Windows slide 7 days forward iteratively.
- Enables temporal adaptation and fault trend analysis.

![Sliding Window diagram.jpg]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/Sliding_window_diagram.jpg))

Fig 3: Sliding Window Diagram.

***

## Results

### Random Forest Result

![Binary CLassification]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/Randf_binary.png))
![Multilabel Classification]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/Randf_multilabel.png))

### XGBoost Result

![Binary CLassification]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/XG_binary.png))
![Multilabel Classification]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/XG_multilabel.png))

#### XGBoost Sliding Windows

##### Precision (Throughout Prediction windows)

![Precision]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/Precision.jpg))

##### Recall (Throughout Prediction windows)

![Recall]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/Recall.jpg))

##### F1-Score (Throughout Prediction windows)

![F1-Score]((https://github.com/imabhivaibhav/atm_predictive_maintenance/blob/64496c01bd64f138336707c1eb6aeb86eacad85f/F1-score.jpg))



## Discussion

- Random Forest excels in training speed and balanced metrics.
- XGBoost offers better recall and detection sensitivity for common faults.
- Both models struggle with rare faults due to class imbalance.
- The sliding window approach captures short-term fault trends effectively.
- Combining binary and multi-label approaches enhances fault screening and diagnosis.

***

## Conclusion and Future Scope

- Both Random Forest and XGBoost provide robust predictive maintenance capabilities.
- Future focus includes improving rare fault detection via synthetic data, deep learning architectures (LSTM, Transformers), and ensembles.
- Integration of multimodal data and continuous learning from operational feedback will strengthen performance.

***

