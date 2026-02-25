# OSC2-RAG-Scenario-Gen

## Retrieval-Augmented Scenario Generation for Autonomous Driving Simulation

This repository contains the research implementation of a
Retrieval-Augmented Generation (RAG) framework for structured autonomous
driving scenario synthesis using **OpenSCENARIO 2 (OSC2)**, integrated
with **Safety Pool conversion** and **CARLA--Autoware co-simulation**.

The project was developed as part of a controlled simulation-based study
comparing three scenario generation paradigms:

-   Template-based generation (prior work baseline)
-   From-scratch LLM generation
-   Retrieval-Augmented Generation (RAG) (proposed method)

This repository documents the pipeline, experimental setup, evaluation
logic, and supporting utilities used in that study.

------------------------------------------------------------------------

## Project Motivation

Autonomous driving systems require structured, diverse, and controllable
safety scenarios for stress testing. Traditional template libraries
provide structural validity but limit diversity. Pure LLM-based
generation increases diversity but often suffers from hallucination and
structural inconsistency.

This work introduces a snippet-level retrieval mechanism that:

-   Grounds generation in reusable OSC2 components
-   Improves structural correctness
-   Enhances diversity while maintaining validity
-   Enables reproducible comparative evaluation

The framework is designed specifically for **simulation-based stress
testing** under a fixed CARLA--Autoware stack. It is not intended as a
real-world safety validation system.

------------------------------------------------------------------------

## What This Repository Contains

This repository includes:

### 1. RAG Pipeline Logic

-   Retrieval of reusable geometry, spawn, and behavior snippets
-   Prompt construction and LLM orchestration
-   Structured OSC2 scenario assembly

### 2. Template-Based Baseline

-   Handcrafted OSC2 scenario templates derived from prior work
-   Used as the controlled baseline for comparison

### 3. From-Scratch LLM Generation

-   Direct natural-language-to-OSC2 generation without retrieval
    grounding
-   Included for ablation comparison

### 4. Snippet Library

-   Modular OSC2 components
-   Geometry primitives
-   Spawn configurations
-   Behavior fragments

These snippets form the retrieval corpus used by the RAG system.

### 5. Safety Pool Conversion Tools

-   Conversion utilities mapping OSC2 scenarios to CARLA-compatible
    execution format
-   Ensures consistency with the evaluation stack

### 6. Evaluation and Metrics

-   Log parsing utilities
-   Composite scoring functions (0--1 scale)
-   Difficulty categorization logic
-   Comparative plotting utilities

The metric design is an engineering heuristic for comparative stress
testing, not a theoretically optimal safety metric.

### 7. Experiment Configurations

-   Scripts and configurations used to reproduce experimental
    comparisons
-   Difficulty alteration experiments
-   Coverage and diversity analysis

------------------------------------------------------------------------

## System-Level Workflow (Conceptual)

Natural Language Prompt\
→ Snippet Retrieval\
→ OSC2 Scenario Synthesis\
→ Safety Pool Conversion\
→ CARLA--Autoware Co-Simulation\
→ Log Collection\
→ Composite Scoring

This repository reflects the implementation of that full pipeline.

------------------------------------------------------------------------

## Scope and Limitations

-   Designed for controlled simulation experiments
-   Evaluated under a fixed CARLA--Autoware stack
-   Baseline comparison limited to prior internal template system
-   Not validated on real vehicles
-   Metrics are comparative engineering heuristics

The framework is intended for structured evaluation research, not
deployment.

------------------------------------------------------------------------

## Research Context

This repository supports a study analyzing:

-   Hallucination reduction via retrieval grounding
-   Structural validity improvements
-   Snippet-level coverage reconstruction
-   Scenario diversity characteristics
-   Controlled difficulty manipulation

All experiments were conducted within a consistent simulation
environment to ensure fairness.

------------------------------------------------------------------------

## Intended Audience

This repository is intended for:

-   Researchers working on LLM-grounded scenario synthesis
-   Autonomous driving simulation researchers
-   Safety validation and stress-testing researchers
-   Developers studying structured generation with retrieval grounding

------------------------------------------------------------------------

## Citation

If you use this repository in academic work, please cite the associated
paper (to be updated upon publication):

@misc{osc2_rag_2026, title={Retrieval-Augmented Scenario Generation for
Autonomous Driving Simulation}, author={Your Name and Coauthors},
year={2026}, note={GitHub repository},
url={https://github.com/BELIV-ASU/osc2-rag-scenario-gen} }

------------------------------------------------------------------------

