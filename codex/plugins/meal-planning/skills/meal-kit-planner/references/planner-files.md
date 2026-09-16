# Planner files

Store household-specific state outside the installed skill so skill upgrades do not overwrite it. The recommended project-relative paths are:

```text
meal-planner/
|-- preferences.yaml
|-- history.csv
`-- reports/
```

## `preferences.yaml`

Use this minimal schema and omit unknown optional values rather than inventing them:

```yaml
meal_count: 5
servings: 2
maximum_calories_per_portion: 599
avoid_within_weeks: 12
maximum_surcharge_per_serving: 0

exclude:
  allergens: []
  ingredients: []
  dietary_labels: []

requirements:
  minimum_vegetarian_meals: 0
  maximum_fish_meals: 5
  maximum_red_meat_meals: 5

preferences:
  favour_high_protein: true
  minimum_protein_grams: null
  favour_quick_meals: false
  maximum_cook_time_minutes: null
  preferred_cuisines: []
  disliked_cuisines: []
```

Treat `exclude` and the calorie, surcharge, meal-count and serving values as hard constraints. Treat `preferences` as ranking signals unless the user explicitly promotes one to a requirement.

## `history.csv`

Use UTF-8 CSV with this header:

```csv
delivery_date,provider,recipe_id,title,calories_per_portion,protein_grams,servings,confirmed_at
```

- `delivery_date`: ISO `YYYY-MM-DD`.
- `provider`: stable lowercase provider name, for example `hellofresh-uk`.
- `recipe_id`: provider recipe UUID or other stable ID when available; leave empty when unavailable.
- `title`: title displayed for the confirmed delivery.
- Nutrition fields: numeric values from that delivery's recipe details, without units.
- `confirmed_at`: ISO 8601 timestamp including timezone.

Append only confirmed selections. Do not record recommendations that were rejected, expired or never saved.

## Weekly reports

Name reports using the ISO week containing the delivery date, for example `reports/2026-W40.md`. A useful report contains:

- delivery date and edit deadline;
- applied hard constraints;
- chosen recipes with calories and protein;
- last-selected date or `never`;
- replacements made and any approved exceptions;
- verification result.

Keep reports concise and free of account identifiers, addresses, payment data and authentication material.
