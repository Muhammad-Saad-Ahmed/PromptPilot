# Project Report: PromptPilot AI
*An Intelligent Prompt Refinement Engine, Evaluation Sandbox, & Educational Coach*

---

## 1. The Idea Behind the Project
Students and novice programmers frequently struggle to get high-quality learning outcomes from advanced AI models (such as Gemini, ChatGPT, or Claude). Their intentions are often written conversationally, in mixed vocabulary, or in localized syntax (like **Roman Urdu** or **Hinglish**). For instance, a student might say: *“Mujhy FastAPI seekhna hai starting stage se”* or *“Explain database joins to me”*.

When passed directly to an AI, these simple requests trigger generic, low-fidelity, and sycophantic replies. The AI often behaves like a "direct code copy-paste vending machine," which robs the student of genuine step-by-step cognitive understanding, critical thinking exercises, and custom-level learning checkpoints.

**PromptPilot AI** solves this problem by acting as an intelligent intermediary. It automatically expands basic, messy intentions into expert, copy-ready, structured prompt blueprints that adhere to **8 hard-coded rules for educational prompt engineering** (including strict anti-slop guidelines, Socratic pedagogical roles, self-scoring rubrics, and iterative feedback loops). It also offers real-time diagnostics, comparative side-by-side simulations of the "ordinary" response versus the "optimized" response, and dynamic target modes (including a specialized **Python Focus Mode**).

---

## 2. The AI-Assisted Development Process
The application was built from scratch using a rapid, full-stack, AI-assisted development workflow:

1. **Architecture Planning**: Chosen a lightweight full-stack runtime using **React 19, TypeScript, Vite, and tailwindcss** for the visual frontend alongside an **Express server** as the backend API proxy.
2. **AI API Orchestration**: Integrated the official, modern `@google/genai` TypeScript SDK on the server side to interface securely with the `gemini-3.5-flash` model, ensuring our API keys are never exposed directly to the student’s web browser.
3. **Iterative Feature Additions**:
   - Built the primary prompt-refinement algorithm using recursive JSON schemas.
   - Built an interactive comparative sandbox executor (`/api/test-run`) that generates live side-by-side trial answers.
   - Customized the application to support localized input (Roman Urdu/Hindi) and added dedicated target modes with a specific **Python Focus Mode** to auto-generate Python-specific constraints, type annotations, and PEP 8 standards.
   - Provided a native Python (`app.py`) mirror implementation of the backend and Streamlit frontend so the entire project can be run natively as a Python-based system.

---

## 3. Prompt Engineering Techniques Used
PromptPilot AI is built *with* prompt engineering and *for* prompt engineering. The core engine applies **8 hard-coded rules of prompting** to any student intention:

*   **Rule 1: Clear Role Assignment (`Act as...`)** - Dynamically assigns a highly specific, trained persona (e.g., *Senior Python Tutor*, *Analytical Database Architect*, *Critical Algorithms Evaluator*).
*   **Rule 2: Explicit Goal Definition (`Your task is...`)** - Focuses the model on detailed educational objectives rather than broad definitions.
*   **Rule 3: Context Buffers (`Background:`)** - Places specific notes, instructions, and placeholders (e.g. `[YOUR SOURCE NOTES HERE]`) to restrict model attention within safe boundaries.
*   **Rule 4: Multi-Layered Constraints (`Do not...`)** - Explicitly tells the AI to *never* give direct code answers immediately, avoid greeting preambles, and omit boilerplate descriptions.
*   **Rule 5: Output Structure (`Format:`)** - Locks response structures into clear steps, exercises, and summaries using markdown components.
*   **Rule 6: Quality Criteria (`Success Criteria:`)** - Outlines exactly what makes a sub-task completed successfully.
*   **Rule 7: Iterative Loop Prompting** - Instructs the AI model to ask critical follow-up questions or set stage challenges for co-collaboration.
*   **Rule 8: Self-Grading Rubrics** - Employs neutral grading standards (1-10 scores) to guide active student improvement objectively.

Additionally, the backend utilizes **Structured Outputs** with the `responseSchema` property in the Gemini API. This ensures the output is returned as highly structured, parseable JSON instead of raw markdown text.

---

## 4. Iterations and Improvements
During development, the prompt-generation guidelines and application layout went through multiple critical phases:

*   **Phase 1: Standard Output Formatting** - Initially returned general markdown prompts. However, the UI lacked analytical depth.
*   **Phase 2: Comparative Scoring Integration** - Added an evaluation panel that grades the Raw User Input against the Generated Prompt across five metrics (Goal Clarity, Context, Output Format, Constraints, Success Criteria) to immediately visualize the value proposition.
*   **Phase 3: Impact-Analysis Diagnostics** - Added diagnostic boxes showing exactly what information was missing from the user's input and how that omission negatively impacts standard AI behavior.
*   **Phase 4: Bilingual Integration** - Enriched the prompt-builder to explicitly recognize Roman Urdu / Hinglish queries, returning prompts that instruct the chatbot to guide and speak with the student using comfortable Roman Urdu mixed with pure coding terms.
*   **Phase 5: Python Focus Mode & Twin Stack** - Added a toggle for Python-optimized prompts and implemented a downloadable Python/Streamlit mirroring script to make the codebase portable to Python-native developers.

---

## 5. Problems Faced and Solutions Applied

*   **Problem 1: Low-Fidelity Responses from Messy Urdu/English Mix Inputs**
    *   *Solution*: Configured the specialized system instructions for the `gemini-3.5-flash` model to act as a Prompt Coach, which actively parses the phonetics of Roman Urdu (e.g., “seekhna hai” -> learn, “mujhy” -> me) and correctly maps them to target computer science topics.
*   **Problem 2: Security Concerns in Iframe with Private API Keys**
    *   *Solution*: Moved all `@google/genai` model requests to an Express server backend. The client browser only calls post routes `/api/generate` and `/api/test-run`. The application secrets are safely stored as an environment variable in container hosting.
*   **Problem 3: Sandboxed Environment Port Conflicts**
    *   *Solution*: Adhered strictly to container network policies by binding the Express server exclusively to host `0.0.0.0` on port `3000`. Combined Vite's development middleware directly inside the Express server sequence so the entire workspace can serve both SPA assets and JSON proxy endpoints on a single port.
*   **Problem 4: Wanting a "Python-Based" App in a NodeJS-Hosted Container**
    *   *Solution*: Added a comprehensive "Python Mode Toggle" in the UI frontend to shape the prompts, and created a dual-language architecture report alongside a complete downloadable `app.py` script replicating the Express and React stack in FastAPI and Streamlit.

---

## 6. Final Working Features
The finalized application delivers a production-grade, highly polished workspace with these key interactive features:

1.  **Dual Input Methods**: Students can pick from classic, localized presets (e.g., FastAPI in Roman Urdu) or write custom raw intentions in any format.
2.  **Adaptive Mode Slider**: Toggles prompt output limits across *Beginner*, *Intermediate*, and *Expert* complexities.
3.  **Topic & Structure Extractor**: The prompt builder extracts the inferred Persona Role, Topic, skill levels, and missing items instantly.
4.  **Copy & Download Actions**: Clear markdown blocks of the generated prompts can be copied instantly or downloaded as raw `.md` documents.
5.  **Side-by-Side Simulation Sub-Sandbox**: Runs a live side-by-side benchmark, showing the direct output of a simple "novice" prompt against the highly precise, pedagogical output of PromptPilot's expanded prompt.
6.  **Interactive Local History**: Automatically stores previous evaluations and generated prompts in the browser's `localStorage` for easy indexing, filtering, and retrieval.
7.  **Fully Documented & Downloadable Report**: The entire system logic is documented right inside the platform and is available for instant reference.
