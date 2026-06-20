<p align="center">
  <img src="https://img.shields.io/badge/Python-3.11+-blue?logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Framework-Streamlit-red?logo=streamlit&logoColor=white" alt="Streamlit">
  <img src="https://img.shields.io/badge/Database-PostgreSQL%20%7C%20SQLite-blue?logo=sqlite&logoColor=white" alt="Database">
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License">
</p>

<h1 align="center">🍽️ WeeklyBite</h1>
<p align="center"><strong>Intelligent Meal Planning & Nutrition Management System</strong></p>

<p align="center">
  <img src="https://raw.githubusercontent.com/streamlit/streamlit/develop/docs/images/streamlit-logo-secondary-colormark-darktext.svg" alt="Streamlit" width="280">
</p>

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Screenshots](#-screenshots)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Usage](#-usage)
- [Configuration](#-configuration)
- [Architecture](#-architecture)
- [Database](#-database)
- [API Reference](#-api-reference)
- [Contributing](#-contributing)
- [License](#-license)

---

## 📋 Overview

**WeeklyBite** is a full-stack meal planning application built entirely in Python using the Streamlit framework. It provides an intelligent weekly meal calendar, automated grocery list generation, personalized macronutrient tracking, and fitness-goal-aligned nutritional guidance — all through a single reactive interface.

### Why WeeklyBite?

Modern meal planning is fragmented across apps, spreadsheets, and paper notes. WeeklyBite solves this by consolidating:

- 🗓️ **Weekly meal scheduling** in a 7-column calendar grid
- 🛒 **Automated grocery list generation** with ingredient deduplication
- 📊 **Personalized nutrition tracking** aligned to your fitness goals
- 💡 **Intelligent insights** that catch nutritional gaps and budget overruns
- 🎨 **Beautiful, customizable themes** for comfortable use

---

## ✨ Features

### 🗓️ Weekly Meal Calendar
- 7-column grid (Mon–Sun) with 3 meal slots per day (Breakfast, Lunch, Dinner)
- Intelligent dropdown menus with real-time meal information
- Visual indicators for dietary category, cuisine type, price, and protein content
- Instant state propagation — every selection updates the entire app

### 🏋️ Fitness Goal Alignment
- Three goal modes: **Cutting** (deficit), **Bulking** (surplus), **Maintenance** (balance)
- BMR calculated via the **Mifflin-St Jeor equation** using your height, weight, age, and gender
- Goal-specific macronutrient splits (protein/carbs/fat ratios)
- Color-coded progress bars: 🟢 within range, 🟠 near boundary, 🔴 out of bounds

### 🔍 Advanced Multi-Criteria Filtering
- **Dietary**: Vegetarian, Non-Vegetarian, Vegan
- **Cuisine**: Indian, Fusion, International
- **Macro Ranges**: Min protein, max carbs, max fat sliders
- **Budget**: Per-meal price ceiling + weekly budget cap
- **Quick Presets**: All, Veg Only, High Protein, Low Carb, Budget
- All filters evaluated simultaneously in a single database query

### 🛒 Intelligent Grocery List
- Real-time ingredient extraction from selected meals
- Automatic deduplication by ingredient name + unit
- Quantity normalization across different units
- Estimated cost per ingredient and total grocery spend
- Categorized display (Proteins, Vegetables, Grains, Dairy, Spices, etc.)
- Copy-to-clipboard export

### 📊 Personalized Nutrition Dashboard
- Daily calorie and macronutrient averages
- Progress bars with target overlays
- Macronutrient split visualization (protein/carbs/fat percentages)
- Day-by-day spending breakdown
- Quick-stat metric cards

### 💡 Insights & Tips Engine
- **8 intelligent rules** that analyze your meal plan:
  - Protein gap detection
  - Budget overrun warnings
  - Calorie deviation alerts
  - Cost-saving substitution suggestions
  - Budget headroom notifications
  - Meal distribution optimization
  - Empty slot reminders
  - Balanced plan positive reinforcement
- Each insight is dismissible, actionable, and scoped to specific days/meals

### 🎨 Theme Customization
- **5 themes**: Light ☀️, Dark 🌙, Forest 🌲, Ocean 🌊, Sunset 🌅
- Instant theme switching with CSS custom properties
- Persistent preference across sessions
- Accessible contrast ratios across all themes

### ✨ Smooth Animations
- 12 keyframe animations (fadeInUp, scaleIn, slideInLeft, bounceIn, pulse, shimmer, floatUp...)
- Staggered card entrances for visual delight
- Hover transforms on all interactive elements
- Progress bar fill animations
- CSS transition utilities

---

## 🖼️ Screenshots

| Calendar | Nutrition | Insights |
|:---:|:---:|:---:|
| Weekly meal grid with smart dropdowns | Progress bars & macro splits | Personalized diet tips |

> *Screenshots will be available in the `/docs/screenshots` directory after running the app.*

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| **Language** | Python 3.11+ |
| **Framework** | Streamlit 1.30+ |
| **Database** | SQLite (dev) / PostgreSQL 15 on Supabase (prod) |
| **UI Components** | Custom CSS + Streamlit native widgets |
| **State Management** | `st.session_state` |
| **Key Libraries** | `pandas`, `numpy`, `sqlite3` |

---

## 📁 Project Structure

```
weeklybite/
├── app.py                        # 🎯 Main application entry point
├── config.py                     # ⚙️  Constants, themes, goal configs
├── run.sh                        # 🚀 Launch script
├── requirements.txt              # 📦 Python dependencies
│
├── database/
│   ├── __init__.py
│   ├── connection.py             # 🔌 SQLite / Supabase unified interface
│   └── seed_data.py              # 🌱 Schema + 73 ingredients + 32 meals
│
├── services/
│   ├── __init__.py
│   ├── nutrition_service.py      # 🧬 BMR, goal thresholds, macro averaging
│   ├── grocery_service.py        # 🛒 Ingredient deduplication, cost calc
│   ├── meal_service.py           # 🍲 Multi-criteria SQL filtering
│   └── insights_engine.py        # 🧠 8 rule-based insight generators
│
├── ui/
│   ├── __init__.py
│   ├── theme.py                  # 🎨 5 themes with CSS custom properties
│   ├── animations.py             # ✨ 12 keyframe animations + transitions
│   └── components.py             # 🧩 Reusable UI components
│
└── utils/
    └── __init__.py
```

---

## 📥 Installation

### Prerequisites

- **Python 3.11 or higher** → [Download Python](https://python.org/downloads/)
- **pip** (comes with Python)

### Step-by-Step

```bash
# 1. Clone the repository
git clone https://github.com/your-username/weeklybite.git
cd weeklybite

# 2. (Optional but recommended) Create a virtual environment
python3 -m venv .venv
source .venv/bin/activate       # Mac / Linux
# .venv\Scripts\activate        # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch the app
streamlit run app.py
```

### Quick Start (No Clone)

```bash
pip install streamlit pandas numpy
cd /path/to/weeklybite
streamlit run app.py
```

---

## 🚀 Usage

### First Launch

1. Open your browser to `http://localhost:8501`
2. The app auto-creates a demo user and seeds the database with **32 meals** and **73 ingredients**
3. No registration needed for development

### Basic Workflow

1. **Set your profile** → Settings tab → enter height, weight, age, gender
2. **Choose your fitness goal** → Settings tab → Cutting / Maintenance / Bulking
3. **Apply filters** → Calendar tab → expand "Filters & Preferences"
4. **Select meals** → Click dropdowns in the 7-column calendar
5. **View your grocery list** → Left sidebar updates instantly
6. **Check nutrition** → Nutrition tab → see progress bars vs. targets
7. **Read insights** → Insights tab → actionable tips and suggestions

### Changing Themes

- Settings tab → Theme section → click any theme pill
- Your preference is saved and persists across sessions

---

## ⚙️ Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `SUPABASE_URL` | Supabase project URL (for production) | `""` (uses SQLite) |
| `SUPABASE_KEY` | Supabase anon/public key (for production) | `""` (uses SQLite) |

### Customizing Goals

Edit `config.py` to adjust:

```python
# Goal multipliers (cutting / maintenance / bulking)
GOAL_MULTIPLIERS = {
    "cutting": 0.80,      # 20% deficit
    "maintenance": 1.00,  # energy balance
    "bulking": 1.15,      # 15% surplus
}

# Macro splits by goal (protein / carbs / fat)
MACRO_SPLITS = {
    "cutting":     {"protein": 0.40, "carbs": 0.30, "fat": 0.30},
    "maintenance": {"protein": 0.30, "carbs": 0.40, "fat": 0.30},
    "bulking":     {"protein": 0.30, "carbs": 0.45, "fat": 0.25},
}
```

---

## 🏗️ Architecture

### Data Flow

```
┌──────────────┐    ┌───────────────────┐    ┌──────────────┐
│   User       │───▶│  Streamlit App    │───▶│  Database    │
│  Interaction │    │  (app.py)         │    │  (SQLite/    │
│              │◀───│                   │◀───│   Supabase)  │
└──────────────┘    └───────┬───────────┘    └──────────────┘
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
        ┌──────────┐ ┌──────────┐ ┌──────────┐
        │Nutrition │ │ Grocery  │ │ Insights │
        │ Service  │ │ Service  │ │ Engine   │
        └──────────┘ └──────────┘ └──────────┘
              │             │             │
              └─────────────┼─────────────┘
                            ▼
                   ┌────────────────┐
                   │  UI Components │
                   │  + Animations  │
                   └────────────────┘
```

### State Management

All application state is managed through `st.session_state`:

```python
st.session_state = {
    'user_metrics':     {...},    # height, weight, age, gender
    'fitness_goal':     '...',    # cutting | maintenance | bulking
    'goal_thresholds':  {...},    # calorie & macro target bands
    'selected_meals':   {...},    # {day: {meal_type: meal_id}}
    'dietary_filters':  [...],    # active dietary categories
    'cuisine_filters':  [...],    # active cuisine types
    'macro_filters':    {...},    # protein/carb/fat ranges
    'price_ceiling':    500.0,    # per-meal max price
    'weekly_budget_cap': 3000.0,  # total weekly budget
    'theme_preference': 'light',  # active theme
    'insights_cache':   [...],    # generated insights
}
```

### Multi-Variable Evaluation

All filters (dietary, cuisine, macro ranges, price) are evaluated in a **single parameterized SQL query**, ensuring UI consistency and eliminating race conditions:

```sql
SELECT m.*, SUM(...) AS total_protein, SUM(...) AS meal_price
FROM meals m
JOIN meal_ingredients mi ON m.id = mi.meal_id
JOIN ingredients i ON mi.ingredient_id = i.id
WHERE m.dietary_category IN (...)
  AND m.cuisine_type IN (...)
GROUP BY m.id
HAVING total_protein BETWEEN ? AND ?
   AND total_carbs <= ?
   AND total_fat <= ?
   AND meal_price <= ?
```

---

## 🗄️ Database

### Schema

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   users     │     │    meals     │     │ ingredients │
├─────────────┤     ├──────────────┤     ├─────────────┤
│ id          │     │ id           │     │ id          │
│ email       │     │ name         │     │ name        │
│ name        │     │ description  │     │ category    │
│ height_cm   │     │ dietary_cat  │     │ unit        │
│ weight_kg   │     │ cuisine_type │     │ cal/unit    │
│ age         │     │ meal_type    │     │ protein/unit│
│ gender      │     │ total_cal    │     │ carbs/unit  │
│ fitness_goal│     │ total_protein│     │ fat/unit    │
│ theme_pref  │     │ total_carbs  │     │ unit_cost   │
│ budget_cap  │     │ total_fat    │     └──────┬──────┘
└──────┬──────┘     │ meal_price   │            │
       │            └──────┬───────┘            │
       │                   │                    │
       │            ┌──────┴───────┐            │
       │            │meal_ingredients│          │
       │            │ id            │          │
       │            │ meal_id ──────┼──────────┘
       │            │ ingredient_id─┼──────────┐
       │            │ quantity      │          │
       │            └───────────────┘          │
       │                                       │
       ▼                                       │
┌──────────────┐                               │
│ weekly_plans │                               │
├──────────────┤                               │
│ id           │                               │
│ user_id      │                               │
│ week_start   │                               │
│ day          │                               │
│ meal_type    │                               │
│ meal_id ─────┼───────────────────────────────┘
└──────────────┘
```

### Seed Data

| Entity | Count |
|--------|-------|
| Ingredients | 73 |
| Meals | 32 |
| Meal-Ingredient Links | 244 |
| Dietary Categories | 3 (Vegetarian, Non-Vegetarian, Vegan) |
| Cuisine Types | 3 (Indian, Fusion, International) |

---

## 📚 API Reference

### Nutrition Service

```python
from services.nutrition_service import (
    compute_goal_thresholds,
    compute_weekly_averages,
    get_deviation_status,
    mifflin_st_jeor_bmr,
)

# Calculate BMR
bmr = mifflin_st_jeor_bmr(weight_kg=75, height_cm=175, age=28, gender="male")
# → 1709.0 kcal

# Get goal thresholds
thresholds = compute_goal_thresholds(75, 175, 28, "male", "cutting")
# → {"calories": {"target": 1367, "min": 1162, "max": 1572}, ...}

# Average your meal plan
averages = compute_weekly_averages(selected_meals)
# → {"daily_calories": 2100, "daily_protein": 120, ...}

# Get color-coded status
status = get_deviation_status(120, thresholds["protein"])
# → "green" | "amber" | "red"
```

### Grocery Service

```python
from services.grocery_service import (
    aggregate_grocery_list,
    compute_weekly_cost,
    compute_weekly_cost_by_day,
)

grocery = aggregate_grocery_list(selected_meals)
# → [{"name": "Rice", "category": "Grains", "total_quantity": 4.5, ...}]

total = compute_weekly_cost(selected_meals)
# → 823.0

daily = compute_weekly_cost_by_day(selected_meals)
# → {"Monday": 224.0, "Tuesday": 230.0, ...}
```

### Meal Service

```python
from services.meal_service import get_eligible_meals, get_meals_grouped

# Filter by all criteria simultaneously
meals = get_eligible_meals(
    dietary_categories=["Vegetarian", "Non-Vegetarian"],
    cuisine_types=["Indian", "Fusion"],
    protein_min=20,
    protein_max=100,
    carbs_max=150,
    fat_max=80,
    price_ceiling=200,
)

# Group by meal type
grouped = get_meals_grouped(...)
# → {"Breakfast": [...], "Lunch": [...], "Dinner": [...]}
```

### Insights Engine

```python
from services.insights_engine import insights_engine

insights = insights_engine.generate(
    plan=selected_meals,
    thresholds=goal_thresholds,
    averages=weekly_averages,
    weekly_cost=823.0,
    budget_cap=3000.0,
    user_goal="maintenance",
)

for insight in insights:
    print(f"[{insight.insight_type}] {insight.title}")
    print(insight.message)
    if insight.action_day:
        print(f"Action: {insight.action_day} {insight.action_meal}")
```

---

## 🔧 Contributing

### Adding New Meals

Edit `database/seed_data.py`:

1. Add ingredient to `SEED_INGREDIENTS` list
2. Add meal to `SEED_MEALS` list
3. Add meal-ingredient mapping to `SEED_MEAL_INGREDIENTS` dict
4. Delete `weeklybite.db` and restart the app

### Adding New Insight Rules

In `services/insights_engine.py`, create a new class:

```python
class MyNewRule(InsightRule):
    priority = 7

    def evaluate(self, plan, thresholds, averages, weekly_cost, budget_cap, user_goal):
        # Your logic here
        if condition_met:
            return Insight(
                insight_type="info",
                title="Your Insight Title",
                message="Detailed message with **markdown** support.",
                priority=self.priority,
            )
        return None
```

Then register it in `InsightsEngine.__init__`: `self.rules.append(MyNewRule())`

### Adding New Themes

Edit `config.py` → `THEMES` dict with your color palette:

```python
"my_theme": {
    "name": "Custom",
    "icon": "🎨",
    "bg_primary": "#...",
    "bg_secondary": "#...",
    # ... all 14 color properties
}
```

---

## 🧪 Testing

```bash
# Run the integration test suite
cd /home/user/weeklybite
python3 -c "
from database.connection import db
from database.seed_data import initialize_database
from services.nutrition_service import compute_goal_thresholds
initialize_database()
thresholds = compute_goal_thresholds(75, 175, 28, 'male', 'maintenance')
print(f'✅ All tests passed! Target: {thresholds[\"calories\"][\"target\"]:.0f} kcal')
"
```

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Streamlit** — for the amazing reactive Python framework
- **Mifflin-St Jeor equation** — the gold standard for BMR estimation
- **Supabase** — for managed PostgreSQL infrastructure

---

<p align="center">
  <strong>🍽️ WeeklyBite</strong> — <em>Plan smarter. Eat better. Live healthier.</em>
</p>

<p align="center">
  Made with ❤️ using Python & Streamlit
</p>