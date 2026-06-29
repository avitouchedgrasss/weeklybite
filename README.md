# WeeklyBite

**A simple, full-stack weekly meal planner** built with Python (Streamlit) and
a Supabase (PostgreSQL) database. Plan your meals for the week, automatically
generate a de-duplicated grocery list, and track calories & macronutrients
against a personalized daily target — all from one simple, single-page app.


---

## Features

| Feature | What it does |
|---|---|
| **Weekly meal grid** | A 7-column calendar (Mon–Sun) with three slots per day (Breakfast / Lunch / Dinner). Pick meals from dropdowns that are filtered live by **dietary** preference (Vegetarian / Non-Vegetarian / Vegan) and **cuisine** (Indian / Fusion / International). Each selected meal shows its calorie & macro breakdown inline. |
| **Save / Load & week navigation** | Persists your plan to the cloud (`weekly_plans` table) per week and per user. Move between weeks with **Prev week / Next week** — every week is saved independently. |
| **Auto grocery list** | Aggregates every ingredient across all selected meals, **de-duplicates by ingredient**, sums quantities, and groups them by category (Vegetables, Proteins, Grains, Spices, etc.). Shows an estimated weekly cost vs. your budget, and exports to a `.txt` file you can take shopping. |
| **Nutrition tracking** | Per-meal nutrition is **computed live** from ingredient data. You get a daily-calorie bar chart plus a carbs / protein / fat breakdown measured against a BMR/TDEE target derived from your profile. |
| **Profile** | Your age, height, weight, gender, and activity level are loaded from the database and are editable. These drive the BMR (Basal Metabolic Rate) and TDEE (Total Daily Energy Expenditure) calorie target. |
| **Reactive UI** | Built on Streamlit's session-state model: change any meal and the grocery list, cost, and nutrition update instantly — no refresh needed. |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | **Python 3.11+** |
| UI framework | **Streamlit** (reactive, server-rendered, Python-native) |
| Database | **PostgreSQL** hosted on **Supabase** (managed, cloud) |
| DB client | `supabase-py` (Python) |
| Config | `python-dotenv` |

**Why this stack?** Both the UI and the data layer are written entirely in
Python. There's no JavaScript frontend, no REST API to build, and no server to
provision — Streamlit handles rendering and Supabase handles storage. This makes
the codebase small, easy to read, and fast to develop.

---

## Project Structure

```
WeeklyBite/
├── app.py              # The entire Streamlit app (UI + logic + DB calls)
├── schema.sql          # Reference of the database tables (documentation only)
├── requirements.txt    # Python dependencies
├── .env                # Your Supabase URL + key (gitignored, not committed)
└── README.md           # This file
```

---

## Getting Started

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Configure your credentials

Create a `.env` file in the project root with your Supabase project's URL and
anon key (already present in this project):

```env
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-anon-public-key
```

> Both values come from your Supabase dashboard, under **Project Settings > API**.

### 3. Run the app

```bash
streamlit run app.py
```

That's it — the app opens in your browser. Because the database tables and data
already exist in your Supabase project, **no additional setup is required**.

---

## How to Use

1. **Set your profile** (left sidebar) — enter age, height, weight, gender, and
   activity level, then click **Save profile**. Your daily calorie target
   (TDEE) updates automatically.
2. **Filter your options** — choose which dietary types and cuisines you want to
   see in the dropdowns.
3. **Plan your week** — for each day, pick a Breakfast, Lunch, and Dinner. As you
   select meals, the calorie/macro readout appears under each slot.
4. **Check your nutrition** — the **Nutrition Summary** section shows a daily
   calorie chart and how your average macros compare to the target.
5. **Build your grocery list** — the **Grocery List** section at the bottom
   auto-generates from your selected meals. Download it as a `.txt` file.
6. **Save** — click **Save plan** to persist the week to the cloud. Use the
   week navigation buttons to plan additional weeks.

---

## How Nutrition Is Calculated

Nutrition is **not stored per meal** — it is **computed at runtime** from the
normalized ingredient tables. For any meal:

```
meal.calories = SUM ( ingredient.quantity * ingredient.calories_per_unit )
meal.protein  = SUM ( ingredient.quantity * ingredient.protein_per_unit  )
meal.carbs    = SUM ( ingredient.quantity * ingredient.carbs_per_unit    )
meal.fat      = SUM ( ingredient.quantity * ingredient.fat_per_unit      )
```

This is summed over every row in `meal_ingredients` belonging to that meal.

**Calorie targets** use the Mifflin–St Jeor equation:

```
BMR (men)   = 10*weight + 6.25*height - 5*age + 5
BMR (women) = 10*weight + 6.25*height - 5*age - 161
TDEE        = BMR * activity_factor
```

**Grocery list de-duplication:** the same ingredient appearing in multiple meals
(e.g. Onion in Monday's breakfast and lunch) is merged into a single line with
its quantities summed, so you never buy the same thing twice.

---

## Database Schema (reference)

Your Supabase project already contains these tables. `schema.sql` documents them
in full. The relationships:

```
users (1) ---- (many) weekly_plans (day_name, meal_type, week_start, meal_id)
                                                     |
meals (1) ---- (many) meal_ingredients (quantity) --+
                           |
ingredients (1) ----------+   (calories/protein/carbs/fat _per_unit, unit_cost, category)
```

| Table | Purpose |
|---|---|
| `meals` | The meal catalog (name, type, dietary category, cuisine, emoji) |
| `ingredients` | Normalized ingredients with per-unit nutrition & cost |
| `meal_ingredients` | Junction table — which ingredients (and how much) each meal uses |
| `weekly_plans` | A user's saved meal selections, keyed by week + day + meal type |
| `users` | User profile (biometrics, preferences, budget) |

---

## Notes & Security

- **Single-user mode:** the app always uses **user id = 1** and has no login
  screen. This keeps things simple. To support multiple users, integrate
  **Supabase Auth** and pass the authenticated user's id instead of the
  hardcoded `1`.
- The `.env` file contains Supabase's **anon (public)** key. This is safe to use
  in client code, but your tables currently use **open Row-Level Security
  policies** — fine for a personal/demo app. Add stricter policies before
  deploying publicly.
- `.env` is listed in `.gitignore` so your key is never committed.

---

## Possible Future Enhancements

- Multi-user accounts with Supabase Auth and per-user data isolation
- Smart meal recommendations based on remaining calorie/macro targets
- One-click grocery ordering via a delivery API integration
- Drag-and-drop meal reordering across days
- Budget breakdown by day and by category

---

## Project Metadata

| Attribute | Details |
|---|---|
| **Technology Stack** | Python 3.11+, Streamlit 1.30+, PostgreSQL 15 (Supabase) |
| **Deployment Target** | Streamlit Community Cloud / local / self-hosted |
| **Architecture** | Monolithic single-page Streamlit app |

---

*WeeklyBite — plan smarter, eat better.*
