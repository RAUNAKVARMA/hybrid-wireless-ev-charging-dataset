#!/usr/bin/env python3
"""
dataset_generator.py

Synthetic Dataset Generator for Hybrid Microwave–Resonant Inductive
Wireless Power Transfer (WPT) in Electric Vehicle Charging Systems.

This script generates a reproducible dataset used to evaluate hybrid
wireless EV charging architectures. It models inductive WPT, microwave
WPT, and a hybrid controller that selects the most efficient mode.

Outputs:
    dataset/hybrid_wpt_dataset.csv

Author: <Your Name>
License: MIT
"""

import os
import numpy as np
import pandas as pd


# ===============================
# Configuration
# ===============================

CONFIG = {
    "samples": 2000,
    "distance_range": (0.10, 0.50),      # meters
    "misalignment_range": (0, 15),       # cm
    "coil_turns_range": (8, 12),
    "frequency_mean": 85,                # kHz
    "frequency_std": 0.8,
    "random_seed": 42
}


# ===============================
# Physical Model Parameters
# ===============================

MODEL = {
    "k0": 0.90,        # max coupling
    "alpha": 3.2,      # coupling decay constant
    "Q_factor": 14     # coil quality factor
}


# ===============================
# Helper Functions
# ===============================

def compute_coupling(distance, misalignment):
    """
    Magnetic coupling coefficient model.
    """
    k0 = MODEL["k0"]
    alpha = MODEL["alpha"]

    coupling_distance = k0 * np.exp(-alpha * distance)

    misalignment_penalty = np.exp(-0.015 * misalignment)

    k = coupling_distance * misalignment_penalty

    return np.clip(k, 0.05, 0.90)


def inductive_efficiency(k, distance, misalignment):
    """
    Inductive wireless power transfer efficiency model.
    """
    Q = MODEL["Q_factor"]

    base = (k**2 * Q**2) / (1 + k**2 * Q**2)
    efficiency = base * 100

    airgap_loss = 25 * distance
    alignment_loss = 0.35 * misalignment
    hardware_loss = np.random.normal(1.8, 0.6)

    eta = efficiency - airgap_loss - alignment_loss - hardware_loss

    return np.clip(eta, 65, 96)


def microwave_efficiency(distance, misalignment):
    """
    Microwave wireless power transfer efficiency model.
    """
    base = 66 + 32 * distance

    beam_penalty = 0.08 * misalignment
    rf_noise = np.random.normal(0, 1.5)

    eta = base - beam_penalty + rf_noise

    return np.clip(eta, 60, 90)


# ===============================
# Dataset Generation
# ===============================

def generate_dataset():
    np.random.seed(CONFIG["random_seed"])

    records = []

    for _ in range(CONFIG["samples"]):

        # --- system parameters ---
        distance = np.random.uniform(*CONFIG["distance_range"])
        misalignment = np.random.uniform(*CONFIG["misalignment_range"])
        turns = np.random.randint(
            CONFIG["coil_turns_range"][0],
            CONFIG["coil_turns_range"][1] + 1
        )

        frequency = np.random.normal(
            CONFIG["frequency_mean"],
            CONFIG["frequency_std"]
        )

        # --- compute coupling ---
        k = compute_coupling(distance, misalignment)

        # --- efficiencies ---
        eta_inductive = inductive_efficiency(k, distance, misalignment)
        eta_microwave = microwave_efficiency(distance, misalignment)

        # --- hybrid controller ---
        eta_hybrid = max(eta_inductive, eta_microwave)

        mode = "Inductive" if eta_inductive >= eta_microwave else "Microwave"

        records.append([
            distance,
            misalignment,
            frequency,
            turns,
            k,
            eta_inductive,
            eta_microwave,
            eta_hybrid,
            mode
        ])

    df = pd.DataFrame(records, columns=[
        "Distance_m",
        "Misalignment_cm",
        "Frequency_kHz",
        "Coil_turns",
        "Coupling_k",
        "Inductive_efficiency",
        "Microwave_efficiency",
        "Hybrid_efficiency",
        "Mode"
    ])

    return df


# ===============================
# Main Execution
# ===============================

def main():

    df = generate_dataset()

    os.makedirs("dataset", exist_ok=True)

    output_path = "dataset/hybrid_wpt_dataset.csv"

    df.to_csv(output_path, index=False)

    print("Dataset generated successfully.")
    print("Saved to:", output_path)
    print("\nFirst 5 rows:\n")
    print(df.head())

    print("\nMode distribution:\n")
    print(df["Mode"].value_counts())


if __name__ == "__main__":
    main()
