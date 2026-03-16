# hybrid-wireless-ev-charging-dataset
Synthetic dataset for hybrid microwave–resonant inductive wireless power transfer in electric vehicle charging systems
# Hybrid Wireless EV Charging Dataset

Synthetic dataset generated for evaluating **Hybrid Microwave–Resonant Inductive Wireless Power Transfer (WPT)** systems for electric vehicle charging.

This dataset supports research on hybrid wireless charging architectures that combine **inductive power transfer (IPT)** and **microwave wireless power transfer (MWPT)** to improve charging efficiency across varying distances and misalignment conditions.

The dataset was generated using a physics-inspired simulation model and is used in the research study:

**"Hybrid Microwave–Resonant Inductive Wireless Power Transfer Architecture for Electric Vehicle Charging Systems"**

---

# Dataset Overview

The dataset contains **2000 operational samples** representing different wireless charging conditions.

Each sample simulates variations in:

- Coil separation distance
- Lateral misalignment between coils
- Resonant operating frequency
- Coil design parameters
- Magnetic coupling coefficient
- Inductive charging efficiency
- Microwave charging efficiency
- Hybrid charging efficiency

The hybrid system dynamically selects the most efficient charging mode.

---

# Dataset Structure

| Column | Description |
|------|-------------|
| Distance_m | Separation between transmitter and receiver coils (meters) |
| Misalignment_cm | Lateral displacement between coils (centimeters) |
| Frequency_kHz | Operating frequency of the resonant system |
| Coil_turns | Number of turns in the transmitter coil |
| Coupling_k | Magnetic coupling coefficient |
| Inductive_efficiency | Efficiency of inductive wireless power transfer (%) |
| Microwave_efficiency | Efficiency of microwave wireless power transfer (%) |
| Hybrid_efficiency | Maximum efficiency achieved between inductive and microwave transfer |
| Mode | Selected charging mode (Inductive or Microwave) |

---

---

# Dataset Generation
code/dataset_generator.py

The dataset was generated using the Python script:
code/dataset_generator.py


The generator simulates wireless power transfer behavior using:

- exponential coupling decay models
- resonant inductive efficiency models
- microwave propagation models
- noise representing real-world system variability

---

# How to Reproduce the Dataset

1. Clone the repository
https://github.com/RAUNAKVARMA/hybrid-wireless-ev-charging-dataset


2. Navigate to the project directory
cd hybrid-wireless-ev-charging-dataset

3. Run the dataset generator
cd hybrid-wireless-ev-charging-dataset


The dataset will be generated in:
dataset/hybrid_wpt_dataset.csv


---

# Example Dataset Sample

| Distance (m) | Misalignment (cm) | Inductive η (%) | Microwave η (%) | Hybrid η (%) | Mode |
|---|---|---|---|---|---|
| 0.12 | 3.2 | 95.7 | 71.3 | 95.7 | Inductive |
| 0.25 | 6.1 | 91.2 | 74.8 | 91.2 | Inductive |
| 0.41 | 10.4 | 83.7 | 78.9 | 83.7 | Inductive |
| 0.48 | 12.7 | 78.5 | 82.1 | 82.1 | Microwave |

---

# Research Applications

This dataset can be used for:

- Wireless power transfer system analysis
- Hybrid charging architecture evaluation
- Efficiency modelling of EV charging systems
- Machine learning based mode selection
- Simulation studies for smart EV charging infrastructure

---

# Citation

If you use this dataset in your research, please cite:
@misc{Varma_Hybrid_Wireless_EV,
author = {Varma, Raunak and Pilania, Ranveer Singh and Shringi, Sakshi},
title = {{Hybrid Wireless EV Charging Dataset}},
url = {https://github.com/RAUNAKVARMA/hybrid-wireless-ev-charging-dataset}
}

---

# License

This dataset is released under the **MIT License** and may be used for research and educational purposes.

---

# Contact

For questions regarding the dataset or simulation model, please contact:
https://github.com/RAUNAKVARMA


