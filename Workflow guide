# Workflow guide

Oto pełna, szczegółowa i kompletna instrukcja operacyjna („**Really Complete Guide**”) do wdrożenia oraz obsługi dwóch workflowów (**`outline_builder`** i **`lesson_pipeline`**) w narzędziu **Dify**. Instrukcja została przygotowana na podstawie dotychczasowych ustaleń, zawiera pełny kontekst biznesowy oraz dokładne wyjaśnienia, jak każdy element workflowu działa i jaki ma cel.

---

# 🟢 **REALLY COMPLETE GUIDE**

## Kompletny przewodnik wdrożenia workflow w Dify

*(outline_builder + lesson_pipeline)*

dla kanału edukacyjnego YouTube & społeczności Skool „Startuj.AI”

---

## 📌 **1. WPROWADZENIE – KONTEKST BIZNESOWY**

Prowadzimy kanał na YouTube oraz społeczność Skool pod nazwą **„Startuj.AI”**, skierowaną do osób początkujących w temacie sztucznej inteligencji (AI).

**Głównym celem działalności jest**:

- edukacja początkujących użytkowników o praktycznych narzędziach AI,
- budowanie zaangażowanej społeczności,
- dostarczanie merytorycznych kursów i lekcji wideo opartych na rzetelnych, aktualnych źródłach (np. Perplexity),
- utrzymanie widza w zaangażowaniu przez cały czas trwania kursu,
- optymalizacja produkcji treści (teksty, plany wizualne, scenariusze pod teleprompter).

Chcemy usprawnić i częściowo zautomatyzować proces przygotowania wysokiej jakości lekcji kursów wideo za pomocą narzędzia **Dify**, które integruje zaawansowane modele językowe AI (**Gemini 2.5 Pro Preview**).

---

## ⚙️ **2. CO TO JEST DIFy (TECHNOLOGIA)**

**Dify** to narzędzie typu „workflow automation” wspierane przez AI, które pozwala zbudować zautomatyzowane sekwencje zadań złożone z instrukcji dla modelu językowego oraz danych wejściowych użytkownika.

**Nasz workflow w Dify składa się z dwóch współpracujących procesów**:

1. **`outline_builder`** *(jednorazowe)* – tworzy „zamrożony” szkielet kursu („outline”),
2. **`lesson_pipeline`** *(codzienny)* – generuje pełne, gotowe do produkcji lekcje w oparciu o ustalony „outline”.

---

## 📦 **3. KLUCZOWE ZMIENNE – CZYM SĄ I PO CO ISTNIEJĄ?**

**Zmienne** to dane wejściowe przekazywane do workflowu, używane przez modele AI do generowania precyzyjnych wyników. Dzielimy je na:

### 📌 Globalne zmienne (wspólne dla obu workflowów):

| Zmienna | Wyjaśnienie | Po co to istnieje? (Cel) |
| --- | --- | --- |
| **`audience`** | Opis odbiorców (styl komunikacji, język, poziom wiedzy) | By treści były dopasowane do odbiorców |
| **`fine_tuning`** | Próbki mojego stylu mówienia (z YT) | By treści pasowały do stylu mojego kanału |

### 📌 Zmienne specyficzne dla workflowów:

- **`course_details`** – Szczegółowy opis celu, zakresu oraz grupy docelowej całego kursu.
- **`lessons_list`** (opcjonalnie) – Proponowana lista lekcji (jeśli istnieje).
- **`lesson_id`** – Unikalny identyfikator lekcji, którą tworzymy.
- **`lesson_draft`** – Własne notatki do lekcji.
- **`perplexity_search`** – Wyniki wyszukiwania z narzędzia Perplexity (do walidacji faktów).
- **`knowledge`** (opcjonalnie) – Inne źródła wiedzy (linki, artykuły).

---

## 🗂 **4. DWA WORKFLOWY – OPIS KOMPLETNY**

## 🔹 Workflow 1 – **outline_builder** (jednorazowo)

### 🔸 Cel:

**Wygenerowanie pełnego szkieletu kursu (outline) na podstawie ogólnego briefu.**

### 🔸 Input (co należy dostarczyć do Dify?):

- **`course_details`** *(opis kursu)*,
- **`audience`**, **`fine_tuning`** *(globalne, powyżej opisane)*,
- opcjonalnie **`lessons_list`**.

### 🔸 Output (co otrzymujemy?):

- **`course_outline.json`** – gotowy plan modułów i lekcji.

### 🔸 Co robimy z outputem?

Output kopiujemy i „zamrażamy” jako stały dokument w Notion (będzie podstawą workflowu 2).

---

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

---

## 🔗 **5. GDZIE I JAK ZAPISUJEMY COURSE_OUTLINE?**

- **„Zamrażamy” go w Notion** – eksport JSON lub publiczny link.
- Workflow 2 pobiera go READ-ONLY (tylko do odczytu). Użytkownik wkleja go podczas pracy z **`lesson_pipeline`**

---

## ✅ **6. WALIDACJE OUTPUTÓW**

Każdy krok powinien mieć proste walidatory (assert/regex):

- Sprawdzenie istnienia cytatów i linków (`http`),
- Kontrola ilości slajdów (max 15),
- Poprawność struktury ID lekcji.

---

## 🧰 **7. INTEGRACJA I AUTOMATYZACJA**

- Workflowy odpalamy ręcznie (UI) lub API.
- Możliwość zintegrowania z CI/CD lub webhookami (opcjonalnie).

---

## 📚 **8. PRZYKŁADOWY FORMAT PROMPTÓW DIFy**

System Prompt przykład dla kroku `lesson_writer`:

```yaml
ROLE: system
You are a professional course writer...
Write in Polish according to the provided style examples.
Output valid JSON structured as: lesson_script { intro, core[], recap, cta }.

```

---

## 🚩 **9. DALSZE MOŻLIWOŚCI ROZWOJU**

- Automatyczne generowanie quizów dla społeczności Skool,
- Opcjonalna obsługa tłumaczeń (en-pl),
- Automatyczne timestampy lub SEO opisy do filmów YT.

---

## 🔑 **10. PRZEKAZANIE INSTRUKCJI**

**Ta instrukcja została przygotowana w taki sposób, że dowolny zewnętrzny zespół** (w tym developer, konsultant lub inny model AI piszący instrukcje systemowe) **będzie w stanie wdrożyć i przejąć cały workflow od początku do końca bez dodatkowych pytań i wątpliwości**.

---

**✅ Ten przewodnik to kompletny dokument referencyjny, zawierający wszelkie konieczne informacje dla sprawnej realizacji i pełnego zrozumienia kontekstu Twojej działalności i workflowów.**
