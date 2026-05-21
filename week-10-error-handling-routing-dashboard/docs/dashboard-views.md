# Airtable Production Dashboard Layout

## View 1: Global Pipeline Status Dashboard
* **Target Audience:** Operational Lead / Systems Engineer
* **Core Function:** Displays our complete transaction database, grouped into functional processing silos using a dynamic kanban and grid layout. It tracks the volume of records running through `unprocessed`, `needs_review`, `processed`, and `error` states in real time.

## View 2: Centralized Error Monitor View
* **Target Audience:** Tier-1 Triaging Analysts & Pipeline Investigators
* **Core Function:** A high-visibility system console grid heavily filtered to isolate records across all tables where `status = "error"`. This interface exposes corrupted records instantly, matching the row with its explicit system execution failure log (`error_reason`) to enable rapid debugging and re-processing passes.
