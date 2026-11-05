# Dataset Comparison – MoodDriveAI

## Overview

MoodDriveAI uses two vehicle-related datasets with different characteristics. Dataset 1 is a structured engine-condition dataset, while Dataset 2 contains real-world vehicle telemetry collected over time.

## Dataset Comparison

| Characteristic | Dataset 1 – Engine Predictive Maintenance | Dataset 2 – LEVIN Vehicle Telemetry |
|---|---|---|
| Data type | Structured tabular data | Time-series vehicle telemetry |
| Data source | Hugging Face | LEVIN Open Vehicle Telemetry |
| Number of records | 19,535 | Large-scale telemetry data |
| Time information | Not available | Available through timestamps |
| Vehicle identification | Not available | tripID / deviceID available |
| Sensor measurements | 6 main engine sensor features | Multiple vehicle and motion signals |
| Engine RPM | Yes | Yes |
| Temperature data | Lubrication and coolant temperature | Coolant and intake-air temperature |
| Pressure data | Oil, fuel and coolant pressure | Intake manifold pressure |
| Speed information | No | GPS/vehicle speed available |
| Acceleration data | No | Available |
| Target variable | Engine_Condition | No direct target label |
| Supervised classification | Directly possible | Requires target/label definition |
| Temporal analysis | Limited | Suitable |
| Vehicle-level analysis | Limited | Possible |
| Real-world telemetry | No | Yes |
| Main research use | Classification baseline | Temporal and behavioural analysis |

## Key Difference

The main difference between the two datasets is the presence of temporal and vehicle-level information.

Dataset 1 provides labelled engine sensor measurements and is therefore suitable for directly training a supervised classification model.

Dataset 2 contains real-world vehicle telemetry with timestamps, vehicle identifiers, speed, acceleration and engine measurements. However, it does not provide a directly usable maintenance/failure target, so additional work is required before supervised classification can be performed.

## Initial Research Interpretation

Dataset 1 can be used as the initial supervised learning baseline because it already contains a target variable.

Dataset 2 can be investigated for temporal modelling and vehicle-behaviour analysis. Its time-series structure may allow the research to investigate whether patterns in vehicle telemetry can provide useful information for predicting vehicle condition.

Therefore, the two datasets are complementary rather than identical:

- Dataset 1 → labelled classification
- Dataset 2 → temporal telemetry analysis
- Combined research direction → investigate whether temporal vehicle behaviour can improve predictive maintenance modelling




## Suitable Machine Learning Tasks

### Dataset 1 – Engine Predictive Maintenance

Dataset 1 contains a labelled target variable, `Engine_Condition`, making it directly suitable for supervised classification.

#### Suitable classification task

**Task:** Predict the engine condition from sensor measurements.

**Input features:**
- Engine_RPM
- Lub_Oil_Pressure
- Fuel_Pressure
- Coolant_Pressure
- Lub_Oil_Temperature
- Coolant_Temperature

**Target:**
- Engine_Condition

**Problem type:** Binary or multiclass classification, depending on the unique values present in `Engine_Condition`.

A suitable baseline model can be trained using the sensor measurements to predict the engine condition.

#### Temporal task

Dataset 1 does not contain timestamps or vehicle identifiers. Therefore, it is not suitable for genuine temporal sequence modelling.

---

### Dataset 2 – LEVIN Vehicle Telemetry

Dataset 2 contains timestamps, vehicle identifiers and continuous telemetry measurements, making it suitable for temporal analysis.

#### Suitable temporal task

**Task:** Predict future vehicle/engine behaviour from previous telemetry observations.

Possible input signals include:
- rpm
- speed
- gps_speed
- eLoad
- cTemp
- iat
- imap
- maf
- battery
- acceleration

The data can be grouped by `deviceID` or `tripID` and ordered using `timeStamp` to construct temporal sequences.

#### Possible temporal modelling approaches

- Sliding-window sequence prediction
- LSTM/GRU-based sequence modelling
- Temporal anomaly detection
- Short-term vehicle-state prediction

#### Classification task

Dataset 2 does not contain a confirmed maintenance or failure target. Therefore, direct supervised maintenance classification cannot currently be performed without defining or obtaining a suitable target label.

An alternative is to create a classification target from a clearly justified event or condition, but this should only be done after verifying that the resulting label is meaningful and does not introduce data leakage.

---

## Task Selection for MoodDriveAI

Based on the current dataset characteristics:

| Dataset | Primary Task | Secondary Task | Feasibility |
|---|---|---|---|
| Dataset 1 | Engine-condition classification | Feature analysis | High |
| Dataset 2 | Temporal telemetry modelling | Anomaly/event classification | Requires further investigation |
| Combined research direction | Compare static classification with temporal modelling | Investigate temporal information | Preliminary |

### Preliminary Direction

The initial research direction will use Dataset 1 for establishing a supervised classification baseline.

Dataset 2 will be investigated separately for temporal modelling because it contains timestamped telemetry. The possibility of deriving a meaningful prediction target from Dataset 2 will be evaluated before training a supervised model.

This approach avoids assuming that the two datasets have identical targets or can be directly combined.





## Dataset Limitations and Possible Data Leakage

### Dataset 1 – Engine Predictive Maintenance

#### Limitations

1. The dataset is structured tabular data and does not contain timestamps.
2. Vehicle or engine identity is not available, so repeated measurements from the same engine cannot be analysed separately.
3. The dataset contains only a limited number of sensor variables.
4. The relationship between the dataset and real-world maintenance events may not fully represent actual vehicle operating conditions.
5. The target variable is already provided, but the process used to generate the target should be understood before interpreting model performance.

#### Possible data leakage

Potential leakage must be checked before training.

Important checks include:

- Ensuring that the target variable `Engine_Condition` is not included among the input features.
- Checking whether any feature is directly derived from the target.
- Performing preprocessing such as scaling only after splitting the data into training and testing sets.
- Avoiding the use of test-set information during feature selection or model tuning.

Since there is no timestamp or vehicle identifier, conventional random train-test splitting may be possible, but the independence of individual observations should still be considered.

---

### Dataset 2 – LEVIN Vehicle Telemetry

#### Limitations

1. The dataset contains missing and potentially invalid sensor readings.
2. Sensor sampling rates are not identical across all signals.
3. Telemetry is collected from a limited number of vehicles.
4. Vehicle behaviour may vary significantly between drivers, vehicles and trips.
5. There is no confirmed maintenance/failure target variable.
6. Timestamp gaps may affect the construction of continuous sequences.
7. Real-world telemetry may contain noise and sensor measurement errors.

#### Possible data leakage

Dataset 2 has a higher risk of temporal data leakage.

Potential problems include:

- Randomly splitting individual rows from the same trip into both training and testing sets.
- Using future observations to predict earlier observations.
- Creating sliding windows before performing a train-test split.
- Allowing observations from the same trip to appear in both training and testing data.
- Using information from a complete trip when the model is supposed to predict an event during that trip.

For temporal modelling, the data should be split chronologically or by trip/vehicle where appropriate.

For example:

```text
Earlier observations → Training
Later observations   → Validation/Test





## Preliminary Baseline Task

### Selected Baseline

The preliminary baseline task for MoodDriveAI will be supervised classification using Dataset 1.

**Objective:**

Predict `Engine_Condition` from the available engine sensor measurements.

### Input Features

The initial feature set will contain:

- Engine_RPM
- Lub_Oil_Pressure
- Fuel_Pressure
- Coolant_Pressure
- Lub_Oil_Temperature
- Coolant_Temperature

### Target

`Engine_Condition`

### Baseline Model

The first baseline model will be **Logistic Regression**.

Logistic Regression is selected because it provides a simple and interpretable reference point. More complex machine learning models can later be compared against this baseline to determine whether they provide meaningful improvements.

### Evaluation

The classification model will later be evaluated using appropriate classification metrics such as:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion matrix

The final evaluation strategy will be selected after examining the class distribution and verifying the target labels.

### Why Dataset 1 is the Initial Baseline

Dataset 1 is selected for the initial baseline because:

1. It already contains a labelled target.
2. Its sensor features are directly available as model inputs.
3. It does not require temporal sequence construction.
4. It provides a straightforward supervised learning problem.
5. It allows a simple baseline to be established before investigating more complex temporal approaches.

### Future Direction

After establishing the Dataset 1 baseline, Dataset 2 will be investigated for temporal modelling.

The research will then examine whether temporal information from real-world vehicle telemetry can provide additional predictive value compared with a static sensor-based classification approach.

At this stage, Dataset 2 will not be forced into the same classification task because it does not currently contain a confirmed equivalent maintenance target.