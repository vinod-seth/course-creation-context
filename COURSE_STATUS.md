# Course Generation Status & Session History

This document serves as the centralized source of truth and memory for all autonomous course generation, guidelines updates, and review tasks. Whenever a new session starts, read this file first to instantly align on the state of all repositories and historical context.

---

## 📋 Course Repository Mapping

The coaching portal registers courses inside the [course-repo](https://github.com/vinod-seth/course-repo.git) `config/` directory. However, actual course materials (MDX tutorials, Jupyter Notebooks, quizzes, and JSON interview questions) are stored in their **respective standalone repositories**. 

| Course ID | Course Title | Standalone Git Repository | Local Workspace Location | Status |
| :--- | :--- | :--- | :--- | :--- |
| `ds-python-basics` | Python Basics | [PythonBasics](https://github.com/vinod-seth/PythonBasics.git) | `c:\vinod\course-repo\PythonBasics` | ✅ Updated |
| `prompt-engineering-mastery` | Prompt Engineering Mastery | [Prompt-Engineering-Mastery](https://github.com/vinod-seth/Prompt-Engineering-Mastery.git) | `c:\vinod\course-repo\Prompt-Engineering-Mastery\Prompt-Engineering-Mastery` | ✅ Updated |
| `slm-development-course` | SLM Development: A Beginner's Guide | [slm-development](https://github.com/vinod-seth/slm-development.git) | `c:\vinod\courses\slm-development` | ✅ Updated |
| `devops-fundamentals-course` | DevOps Fundamentals | [devops-fundamentals](https://github.com/vinod-seth/devops-fundamentals.git) *(Private/Uncreated)* | `c:\vinod\course-repo\DevOps` | ⏳ Pending (Leave as is) |
| `cloud-azure-ai` | Azure AI | `azure-ai-content` | N/A (Not created/cloned) | ⏳ Pending |
| `cloud-azure-dev` | Azure Developer | `azure-dev-content` | N/A (Not created/cloned) | ⏳ Pending |
| `ds-python-etl` | ETL Processes | `python-etl-content` | N/A (Not created/cloned) | ⏳ Pending |

---

## 🛠️ Session Work Log (June 30, 2026)

### Objective
Replace generic/templated interview question placeholders in existing course directories with highly specific, practical, theoretical, and design questions that map directly to real-world scenarios and specific lesson structures.

### Completed Work

#### 1. DevOps Course
*   **Instruction**: User directed to leave DevOps as-is for now, since it does not have a separate respective repository configured and accessible yet.
*   **Action**: Reverted all DevOps changes in the local workspace, restoring `DevOps/tutorial/` back to its original clean state from commit `7d9feb0`.

#### 2. Prompt Engineering Mastery
*   **Action**: Generated 11 chapter-specific questions and a comprehensive course suite.
*   **Curriculum Mapping**: Topics cover tokenization architectures (Tiktoken vs. SentencePiece), temperature/Top-P scaling, Stanford's "Lost in the Middle" research, vector embeddings similarity (RAGAS), function calling schemas, dual-model guardrails, prompt chaining orchestrators, and gateway API load-balancing.
*   **Repository Promotion**: Pushed directly to [Prompt-Engineering-Mastery](https://github.com/vinod-seth/Prompt-Engineering-Mastery.git).

#### 3. Python Basics
*   **Action**: Generated 15 chapter-specific questions and a comprehensive course suite.
*   **Curriculum Mapping**: Topics cover mutable vs. immutable objects, CPython small integer caching pool (-5 to 256), string interning (`sys.intern`), list growth factor pre-allocations, open addressing probing collision resolutions, C3 Linearization Method Resolution Order (MRO), custom validation descriptors, exception chaining (`raise from`), zero-cost exception tables, and dynamic loaders (`sys.meta_path`).
*   **Repository Promotion**: Pushed directly to [PythonBasics](https://github.com/vinod-seth/PythonBasics.git).

#### 4. course-repo Housekeeping
*   **Action**: Untracked all course content folders (`DevOps/`, `Prompt-Engineering-Mastery/`, `PythonBasics/`) from the `course-repo` main repository. Committed and pushed this clean-up.
*   **Result**: The `course-repo` repository on GitHub now exclusively tracks configuration files inside the `config/` directory and documentation files like `README.md`, keeping it lightweight and dedicated strictly to index manifests.

---

## 🔍 Validation & Verification Protocol

Before pushing any interview questions/metadata JSON to a repository, execute a validation pass:
1.  **JSON Validation**: Ensure files parse correctly without syntax errors.
2.  **Schema Check**: Every question file must have a `lesson_title` and an `experience_levels` mapping (`junior`, `mid_level`, `senior`).
3.  **Required Fields**: Ensure each question object has `id`, `question`, `complexity`, `companies`, `core_intent`, `preparation_guide`, `explanation`, `star_framework_tip`, `common_pitfalls`, and `references`.
4.  **No Placeholders**: Scan for keywords such as "placeholder", "todo", "templating", "insert here" or "lorem ipsum" to verify strict adherence to custom production content.

---

## 🚀 Guidelines to Run Updates Across All Courses

When review guidelines or course standards change, use the following execution flow:

```mermaid
flowchart TD
    A[Detect Guideline/Schema Change] --> B[Clone/Pull target respective repository]
    B --> C[Verify current local environment configuration]
    C --> D[Identify files needing modification]
    D --> E[Inject or rewrite tailored technical questions aligning with lesson topic]
    E --> F[Run local validation script to check JSON syntax, schema, and placeholders]
    F --> G|Success| H[Stage, commit, and push directly to respective repo main branch]
    F -->|Failure| I[Refine generated content and re-run check]
```

### Key Checklist for Updates
*   [ ] Read the updated guidelines from the guidelines repository.
*   [ ] Make changes locally in the course's respective standalone folder.
*   [ ] Never commit or stage course contents to `course-repo` (only update `config/` files there if registering/deregistering courses).
*   [ ] Verify changes are pushed directly to the specific standalone GitHub repository.
