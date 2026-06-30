# REDROB_AI-HACKATHON_SUBMISSION-
RedRob AI: Intelligence Engine

🧠 High-Precision, Hallucination-Free Candidate Screening

RedRob AI is a decoupled, multi-stage machine learning pipeline designed to process high-volume unstructured resume data to identify top-tier ML Engineering talent. Unlike traditional keyword-based systems, our engine utilizes LLM-driven evidence reasoning, cross-encoder reranking, and dynamic ensemble math to simulate a senior recruiter’s decision-making process at scale.

# COLAB NOTEBOOK HAS THE WHOLE CODE AND GOOGLE DRIVE LINK INSIDE MAKE SURE TO ADD SHARED FOLDER ADD INSIDE YOUR EVALUATING SYSTEM GOOGLE DRIVE

# AS PART OF TRANSPERANCY WE HAVE SHARED ONE ANOTHER SUBSIDARY NOTEBOOK WHICH WAS ORIGNALLY USED BY OUR TEAM(RAW NOTEBOOK)--THIS NOTEBOOK HAS SINGLE CELL SHARED PIPELINE WHILE THE FINAL SUBMISSION IS DECOPULED REPLICA OF SAME..

📂 Shared Drive Access

For ease of implementation and immediate reproducibility, a shared Google Drive folder is provided containing all pre-downloaded models, datasets, and JD configuration files. Please ensure this drive is mounted in your environment before executing the pipeline to ensure seamless access to all assets.

🏗️ Architecture Overview

The system is architected as a decoupled, modular pipeline. This modularity is not just for organization—it is a critical engineering decision to maximize GPU memory safety and ensure OOM-free execution on constrained environments like Google Colab.

The 5-Phase Pipeline

Phase 0 (JD Intelligence): Contextualizes the Job Description to define target skill sets, implicit signals, and critical disqualifiers.

Phase 1A/B (Extraction & Reasoning): Performs high-throughput mass extraction followed by deep contextual reasoning to hunt for concrete deployment evidence (e.g., "shipped," "latency," "QPS").

Phase 1C (Vector Ingestion): Converts enriched candidate profiles into a 1024-dimensional semantic space, utilizing disk-based HNSW indexing for infinite scalability.

Phase 2 (Cascade Reranking): Leverages a decoupled Cross-Encoder (bge-reranker) to detect nuance in candidate text compared to the JD.

Phase 3 (Ensemble & Reasoning): Applies a weighted executioner equation (Semantic + Reranker + Behavioral + Extraction) followed by LLM-based Chain-of-Thought reasoning.

🚀 Key Features

Anti-Hallucination Guardrails: Phase 1A is intentionally "blindfolded" to JD keywords during extraction, ensuring we extract facts, not buzzwords.

Memory-Safe Scaling: By leveraging qdrant on-disk storage and decoupled Python executables, the pipeline clears GPU memory between stages, preventing crashes.

Dynamic MinMax Reranking: Replaces arbitrary score compression with batch-variance-aware normalization, allowing Tier 1 talent to clearly separate from Tier 3 candidates.

Business Constraint Logic: Applies geographic and notice-period nudges as a final "Executioner" step, ensuring the pipeline maintains technical integrity while respecting hiring constraints.

⚙️ Installation & Requirements

Dependencies

Ensure you have a GPU environment with the following dependencies:

pip install vllm qdrant-client sentence-transformers json-repair python-docx pandas numpy transformers


Execution

The pipeline is designed to be executed as a series of isolated processes:

# 1. Extraction, Reasoning, and Vector Ingestion
python phase1_pipeline.py

# 2. Semantic Retrieval (Top 150)
python retrieve_top150.py

# 3. Cross-Encoder Reranking
python reranker.py

# 4. Final Ensemble & Submission
python submission.py


🛠️ Configuration

Adjust parameters in the configuration block of phase1_pipeline.py:

IS_TEST_RUN: Toggle between True (for dev) and False (for production).

TEST_LIMIT: Number of candidates to process in test mode.

JD_CORE_SKILLS: Custom set of core technical competencies for the engine.

📝 License

This project is proprietary and confidential.

Built with Qwen2.5-Instruct, vLLM, BGE-M3, and Qdrant.
