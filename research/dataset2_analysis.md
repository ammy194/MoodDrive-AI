# MoodDrive AI – Dataset 2 Exploration

## 1. Dataset Information
- Dataset: LEVIN Open Vehicle Telemetry
- Source: Kaggle
- Original files: allcars.csv and v2.csv
- File analysed: allcars.csv
- Format: CSV
- Columns inspected: 18

## 2. Sensor Signals Identified
- GPS speed
- Battery voltage
- Engine load
- Engine RPM
- Accelerometer data
- Coolant temperature
- Intake air temperature
- Mass air flow
- Fuel efficiency

## 3. Timestamp Analysis
- Timestamps successfully converted to datetime.
- Typical sampling interval: 1 second.
- Typical sampling frequency: 1 Hz.
- A 2-second interruption was identified.
- A large gap of approximately 9 days was
  identified within the first 1000 records.

## 4. Missing Value Analysis
Several columns contained entirely missing values
in the inspected 1000-row sample, including:
- Coolant temperature
- Diagnostic trouble codes
- Intake air temperature
- Intake manifold pressure

These require further investigation.

## 5. Sensor Visualisation
Plotted:
- GPS speed over time
- Battery voltage over time
- Engine load over time

A 300-record sample was used for detailed visualisation.

## 6. Data Quality Findings
- GPS speed contained 92% zero values.
- Battery contained 51% zero values.
- Engine load contained 51.33% zero values.
- Battery and engine load simultaneously
  dropped to zero at record index 147.
- These readings may indicate invalid telemetry
  or recording interruptions.

## 7. Initial Conclusion
The LEVIN dataset provides useful vehicle
telemetry signals for studying vehicle behaviour.

However, timestamp discontinuities, missing
values and suspicious zero readings must be
investigated before model development.

Further preprocessing and sensor validation
will be required.