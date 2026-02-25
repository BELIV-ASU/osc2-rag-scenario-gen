OSC2-RAG-Scenario-Gen

Retrieval-Augmented Scenario Generation for Autonomous Driving Simulation (OSC2 + CARLA–Autoware)

Official implementation of our RAG-based scenario synthesis and evaluation framework for autonomous driving simulation using OpenSCENARIO 2 (OSC2), Safety Pool conversion, and CARLA–Autoware co-simulation.

This repository provides a modular pipeline to generate, validate, execute, and evaluate safety-critical driving scenarios from natural language prompts.

🚀 Overview

Autonomous driving systems require diverse, structured, and controllable safety scenarios for stress testing. Traditional template-based generation is rigid and limited in diversity, while naïve LLM generation suffers from hallucination and structural invalidity.

This project introduces a Retrieval-Augmented Generation (RAG) framework that:

Grounds scenario synthesis in reusable OSC2 snippets

Reduces hallucinations and structural errors

Improves scenario diversity and validity

Supports Safety Pool → CARLA conversion

Enables reproducible evaluation under a fixed CARLA–Autoware stack

We compare:

Template-based generation (baseline)

From-scratch LLM generation

RAG-based generation (proposed)

🏗 System Architecture
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
Key Features

📚 Snippet-level retrieval grounding

🧱 Structured OSC2 scenario construction

🔁 Automatic Safety Pool conversion

🚘 Closed-loop CARLA–Autoware evaluation

📊 Composite SafeBench-style scoring

⚖ Controlled difficulty manipulation

📂 Repository Structure (High-Level)
osc2-rag-scenario-gen/
│
├── rag_pipeline/              # Retrieval + LLM orchestration
├── osc2_templates/            # Baseline template library
├── snippet_library/           # Geometry / spawn / behavior snippets
├── safety_pool_converter/     # OSC2 → CARLA conversion tools
├── evaluation/                # Scoring & metrics
├── experiments/               # Reproducible experiment configs
├── figures/                   # Paper figures
├── scripts/                   # Run scripts
└── README.md

(Adjust this section if your folder names differ.)

🔧 Requirements
Core Dependencies

Python 3.10+

CARLA (tested on recommended project version)

Autoware (version used in paper)

OpenSCENARIO 2 toolchain

OpenAI API (or compatible LLM API)

Install Python dependencies:

pip install -r requirements.txt
⚙️ Setup
1️⃣ CARLA

Start CARLA server:

./CarlaUE4.sh
2️⃣ Autoware

Launch Autoware in simulation mode.

3️⃣ Environment Variables

Set your LLM API key:

export OPENAI_API_KEY="your_key_here"
🧠 Running Scenario Generation
RAG-Based Generation
python scripts/run_rag_generation.py \
    --prompt "A vehicle cuts in aggressively during lane merge" \
    --output_dir outputs/rag/
Template-Based Baseline
python scripts/run_template_generation.py \
    --template_id lane_cut_in \
    --output_dir outputs/template/
From-Scratch LLM
python scripts/run_llm_generation.py \
    --prompt "..." \
    --output_dir outputs/llm/
🚘 Running Simulation & Evaluation
python scripts/run_simulation.py \
    --scenario outputs/rag/scenario.osc2

After simulation:

python scripts/compute_metrics.py \
    --log_dir logs/scenario_X/

Outputs include:

Ego trajectory logs

Collision events

Route completion

Composite difficulty score (0–1 scale)

📊 Evaluation Metrics

Our scoring system is an engineering heuristic for comparative stress testing, not a theoretically optimal safety metric.

Composite score components may include:

Route completion ratio

Collision penalty

Deadlock detection

Lane deviation

Traffic rule violations

The framework is intended for:

Controlled, simulation-based comparative evaluation under a fixed CARLA–Autoware stack.

It is not a real-world safety validation system.

🔬 Reproducing Paper Results

To reproduce the comparative study:

python experiments/run_full_comparison.py

This will:

Generate scenarios under all three strategies

Execute simulations

Compute metrics

Produce plots used in the paper

⚠️ Scope & Limitations

Designed for simulation-only stress testing

Evaluated under a fixed CARLA–Autoware stack

Baseline comparison limited to our prior template system

Not validated on real vehicles

Metric design is heuristic and comparative

📖 Citation

If you use this work, please cite:

@misc{yourcitation2026,
  title={Retrieval-Augmented Scenario Generation for Autonomous Driving Simulation},
  author={Your Name and Coauthors},
  year={2026},
  note={GitHub repository},
  url={https://github.com/BELIV-ASU/osc2-rag-scenario-gen}
}

(Replace with your final published BibTeX.)

🤝 Contributing

Pull requests are welcome.
For major changes, please open an issue first to discuss proposed modifications.

📬 Contact

For questions regarding the framework:

Your Name – Arizona State University

Lab: BELIV Lab

GitHub Issues preferred for technical questions

📝 License

Specify your license here (e.g., MIT, Apache 2.0, etc.)
