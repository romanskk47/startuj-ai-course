## 🔹 Workflow 2 – **lesson_pipeline** (codzienny)

### 🔸 Cel:

**Tworzenie pojedynczych, kompletnych lekcji gotowych do nagrania na bazie zamrożonego „outline”.**

### 🔸 Krok po kroku (steps w Dify):

| Krok | Co robi? | Input (wejścia) | Output (wyjścia) |
| --- | --- | --- | --- |
| 1 | **lesson_planner** | `lesson_id`, `course_outline`, `lesson_draft` | `lesson_spec` – cele lekcji, hooki, struktura |
| 2 | **research_hub** (walidacja faktów) | `lesson_spec`, `perplexity_search`, `knowledge` | `curated_sources` – cytaty i źródła |
| 3 | **lesson_writer** (pisanie lekcji) | `lesson_spec`, `curated_sources`, `fine_tuning` | `lesson_script` – skrypt lekcji |
| 4 | **visual_director** (plany wizualne, źródła, pozyskane w trakcie **research_hub** materiały interaktywne) | `lesson_script` | `visual_plan` – scenariusz wizualny |
| 5 | **teleprompter_packager** (prompter) | `lesson_script`, `visual_plan` | `prompter_script` – gotowy tekst na prompter |
