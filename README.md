# OSC2-RAG-Scenario-Gen

**Retrieval-Augmented Scenario Generation for Autonomous Driving
Simulation (OSC2 + CARLA--Autoware)**

Official implementation of our RAG-based scenario synthesis and
evaluation framework for autonomous driving simulation using
**OpenSCENARIO 2 (OSC2)**, **Safety Pool conversion**, and
**CARLA--Autoware co-simulation**.

------------------------------------------------------------------------

## 🚀 Overview

Autonomous driving systems require diverse, structured, and controllable
safety scenarios for stress testing. Traditional template-based
generation is rigid and limited in diversity, while naïve LLM generation
suffers from hallucination and structural invalidity.

This project introduces a **Retrieval-Augmented Generation (RAG)**
framework that:

-   Grounds scenario synthesis in reusable OSC2 snippets\
-   Reduces hallucinations and structural errors\
-   Improves scenario diversity and validity\
-   Supports Safety Pool → CARLA conversion\
-   Enables reproducible evaluation under a fixed CARLA--Autoware stack

We compare:

1.  **Template-based generation (baseline)**\
2.  **From-scratch LLM generation**\
3.  **RAG-based generation (proposed)**

------------------------------------------------------------------------

## 🏗 System Architecture

    Natural Language Prompt
              ↓
       Snippet Retrieval (RAG)
              ↓
        OSC2 Scenario Synthesis
              ↓
     Safety Pool Conversion
              ↓
     CARLA–Autoware Co-Simulation
              ↓
       Log Collection + Scoring

------------------------------------------------------------------------

## 📂 Repository Structure

    osc2-rag-scenario-gen/
    │
    ├── rag_pipeline/              
    ├── osc2_templates/            
    ├── snippet_library/           
    ├── safety_pool_converter/     
    ├── evaluation/                
    ├── experiments/               
    ├── figures/                   
    ├── scripts/                   
    └── README.md

------------------------------------------------------------------------

## 🔧 Requirements

-   Python 3.10+
-   CARLA (project-tested version)
-   Autoware (project-tested version)
-   OpenSCENARIO 2 toolchain
-   OpenAI API (or compatible LLM API)

Install dependencies:

``` bash
pip install -r requirements.txt
```

------------------------------------------------------------------------

## ⚙️ Setup

### Start CARLA

``` bash
./CarlaUE4.sh
```

### Launch Autoware

Start Autoware in simulation mode.

### Set API Key

``` bash
export OPENAI_API_KEY="your_key_here"
```

------------------------------------------------------------------------

## 🧠 Running Scenario Generation

### RAG-Based

``` bash
python scripts/run_rag_generation.py     --prompt "A vehicle cuts in aggressively during lane merge"     --output_dir outputs/rag/
```

### Template-Based

``` bash
python scripts/run_template_generation.py     --template_id lane_cut_in     --output_dir outputs/template/
```

### From-Scratch LLM

``` bash
python scripts/run_llm_generation.py     --prompt "A vehicle cuts in aggressively during lane merge"     --output_dir outputs/llm/
```

------------------------------------------------------------------------

## 🚘 Simulation & Evaluation

Run simulation:

``` bash
python scripts/run_simulation.py     --scenario outputs/rag/scenario.osc2
```

Compute metrics:

``` bash
python scripts/compute_metrics.py     --log_dir logs/scenario_X/
```

Outputs include:

-   Ego trajectory logs\
-   Collision events\
-   Route completion ratio\
-   Composite difficulty score (0--1 scale)

------------------------------------------------------------------------

## 📊 Evaluation Philosophy

The scoring system is an **engineering heuristic for comparative stress
testing**, not a theoretically optimal safety metric.

This framework is intended for:

> Controlled, simulation-based comparative evaluation under a fixed
> CARLA--Autoware stack.

It is **not** a real-world safety validation system.

------------------------------------------------------------------------

## 🔬 Reproducing Paper Results

``` bash
python experiments/run_full_comparison.py
```

------------------------------------------------------------------------

## ⚠️ Scope & Limitations

-   Designed for simulation-only stress testing\
-   Evaluated under a fixed CARLA--Autoware stack\
-   Baseline comparison limited to prior template system\
-   Not validated on real vehicles\
-   Metric design is heuristic and comparative

------------------------------------------------------------------------

## 📖 Citation

``` bibtex
@misc{osc2_rag_2026,
  title={Retrieval-Augmented Scenario Generation for Autonomous Driving Simulation},
  author={Your Name and Coauthors},
  year={2026},
  note={GitHub repository},
  url={https://github.com/BELIV-ASU/osc2-rag-scenario-gen}
}
```

------------------------------------------------------------------------

## 🤝 Contributing

Pull requests are welcome. Please open an issue first to discuss major
changes.

------------------------------------------------------------------------
