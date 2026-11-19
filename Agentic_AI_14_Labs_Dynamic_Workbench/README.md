# Agentic AI Course Organizer — One Integrated Assistant, 14 Capabilities

A FastAPI + SQLite academic management application with student and professor dashboards. The fourteen Agentic AI lab concepts are implemented as capabilities behind one Academic AI Assistant. Users enter a request once; the orchestrator selects and runs relevant components. There are no separate lab launch buttons or a separate lab showcase page in the application UI.

## Main application features

- Student/professor login and role-based access.
- Courses, enrolments, notes and versions, assignments, submissions, milestones, grading, grade approval/publication and audit history.
- One Academic AI Assistant available to student and professor accounts.
- Natural-language routing to the relevant integrated lab capability.
- Execution details show the capability selected, components actually invoked, status, tool details and structured output.
- Student academic retrieval remains scoped to the authenticated student's own enrolled courses and records. Professor data views are limited to courses in the professor's teaching scope where that scope is available.

## The 14 integrated capabilities

1. **Agent vs Chatbot** — text-only baseline compared with a tool-selecting agent.
2. **Tool-Using Agent** — safe calculator, course lookup and text-analysis tools.
3. **Reusable Skills** — discover, create/version and execute supported reusable skills.
4. **Memory & Retrieval** — persistent user-scoped memory; explicit remember/recall requests.
5. **Connectors** — discover and invoke registered academic database, sandboxed workspace and HTTPS connectors. This is an internal connector registry, not a full official MCP SDK server.
6. **Agent Runtime** — lifecycle events and local execution status.
7. **Agentic Node Graph** — dependency-aware graph execution with cycle/unknown-dependency validation.
8. **Parallel Agent Swarm** — concurrent deterministic Python specialist workers; these are not independent LLM agents.
9. **Deep Research** — evidence brief from the bundled local corpus and user-supplied evidence. It is not live internet research.
10. **Cloud Operations** — log classification and safe remediation recommendations. It does not operate real cloud infrastructure.
11. **Agentic SDLC** — requirement-specific user stories, acceptance criteria, test matrix and lifecycle planning artifacts; it does not deploy production code.
12. **Safety & Governance** — validation, audit and persistent human-approval records. Approval does not execute a production action.
13. **Engineering Specialists** — mechanical, civil and electrical sensor-data analysis with configurable/illustrative thresholds. Thresholds are not certified engineering limits.
14. **Capstone Project Studio** — persistent helpdesk triage and ticket lifecycle.

Capabilities are demand-driven. A normal academic question does not claim that unrelated labs ran. The execution trace records only components actually invoked. To demonstrate each capability, enter a suitable natural-language request or structured JSON payload in the same assistant input.

## Windows setup

1. Extract the ZIP and open the project root in VS Code.
2. Open Terminal → New Terminal.
3. Create and activate a virtual environment:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

4. Install dependencies:

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

5. Start the application:

```powershell
python -m uvicorn course_organizer.main:app --host 127.0.0.1 --port 8002 --reload
```

6. Open `http://127.0.0.1:8002/` and log in.

`START_APPLICATION.bat` performs dependency installation and starts the server. Keep its terminal window open while using the application.

## Demo accounts

- Student: `test.student@example.com` / `student123`
- Professor: `test.professor@example.com` / `professor123`

Change demo passwords and set `COURSE_ORGANIZER_SECRET` before exposing the application beyond a local demonstration.

## Demonstration prompts (all through the same assistant)

- Lab 1: `Compare a chatbot and an agent for finding courses.`
- Lab 2: `Calculate 125 * 8.`
- Lab 3: `List skills.` To create a skill, submit JSON: `{"action":"create","name":"upper_text","description":"Uppercase text","operation":"uppercase"}`. To run: `{"action":"run","name":"upper_text","input":"hello"}`.
- Lab 4: `Remember that I prefer concise explanations.` Then: `What do you remember about my preferences?`
- Lab 5: `List available connectors.`
- Lab 6: `Show runtime events for calculating 25 + 17.`
- Lab 7: submit JSON with a `nodes` array, for example: `{"nodes":[{"id":"a","operation":"word_count","input":"hello world"},{"id":"b","operation":"uppercase","input":"agent","depends_on":["a"]}]}`.
- Lab 8: `Run parallel specialist analysis on this text: student scores improved but one assignment failed.`
- Lab 9: `Research artificial intelligence applications in education.`
- Lab 10: `Analyse these cloud logs: INFO service started; ERROR database connection timeout.`
- Lab 11: `Generate an SDLC test plan for a library management system.`
- Lab 12: submit structured JSON with `diagnosis`, `proposed_change`, `rollback_plan`, `privacy_scrubbed`, `estimated_cost` and `budget`.
- Lab 13: `Analyse civil engineering sensor readings: crack_width_mm=0.5` on one line and `displacement_mm=12` on the next.
- Lab 14: `Create ticket for campus portal login failure.` The assistant scopes the ticket to the authenticated user.

## Tests

Run from the project root:

```powershell
.\RUN_TESTS.bat
```

Or run the focused Python suites:

```powershell
python -m unittest tests.test_agentic_core tests.test_all_14_dynamic tests.test_labs_9_14 tests.test_unified_assistant -v
python -m unittest course_organizer.database.test_db_service course_organizer.database.test_extended_db_service course_organizer.agents.test_integrated_lab_agent -v
python -m unittest lab3.test_skills lab4.test_memory lab5.test_connectors lab6.test_runtime lab7.test_graph lab8.test_swarm -v
```

## Important scope and safety notes

- The assistant is a deterministic local agent orchestrator with rule-based routing and registered tools; it is not an LLM unless an explicitly configured LLM endpoint is used by the academic assistant.
- Connector integration is an internal registry abstraction, not a full official MCP SDK implementation or stdio MCP server.
- Parallel specialist execution uses concurrent Python workers, not autonomous LLM agents.
- Research uses local bundled evidence and clearly attributed user-supplied evidence; no live web crawling is claimed.
- Cloud operations only diagnoses supplied logs and recommends actions; it does not change cloud resources.
- SDLC outputs are planning/test artifacts, not production code deployment.
- Engineering thresholds are illustrative and must be replaced with site-approved limits before real-world use.
- Governance approvals record a human decision and do not execute production actions.
- Keep the bundled Course Organizer database. The agentic core stores its separate persistent state in `course_organizer/database/agentic_core.sqlite3`.

## Project structure

- `course_organizer/` — existing academic management application and domain agents.
- `course_organizer/agents/unified_agent.py` — single assistant entry point and capability router.
- `agentic_core/` — shared runtime, tools, memory, connector registry, approvals and execution persistence.
- `lab1/` … `lab14/` — lab-specific capability implementations and tests.
- `tests/` — shared-core, dynamic capability and unified-assistant tests.

## One-command 14-lab demonstration
Open the Academic AI Assistant and enter `Run the 14-lab demonstration suite`. This executes one transparent demonstration worklet per lab (plus stateful follow-up steps for skills, memory, and connectors), records each run in SQLite, and returns a trace with statuses and run IDs. See `DEMO_PRESENTATION_SCRIPT.md` for individual prompts and implementation boundaries.
