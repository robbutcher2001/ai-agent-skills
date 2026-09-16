---
name: meal-kit-planner
description: Review an upcoming meal-kit menu, filter recipes by dietary requirements, avoid recent repeats, recommend a balanced set, optionally update the order after explicit approval, and record confirmed selections. Use for recurring HelloFresh or similar meal-kit planning; do not use for general recipe discovery unrelated to an account menu.
---

# Meal Kit Planner

Build a reviewable weekly meal plan from the user's live meal-kit menu and their version-controlled preferences and history.

## Locate planner state

Look for `meal-planner/preferences.yaml` and `meal-planner/history.csv` in the current repository or a location supplied by the user. Read [references/planner-files.md](references/planner-files.md) before creating or changing either file.

If no preference file exists, inspect the live menu read-only and ask only for missing hard constraints that would materially affect eligibility, such as allergens, prohibited ingredients, calorie ceiling, meal count, or surcharge policy. Offer to create the planner files after those values are known.

Never store passwords, session cookies, addresses, payment details, tokens, or other account credentials in planner files or Git.

## Plan a delivery

1. Identify the intended delivery and its edit deadline. Do not assume that “next week” maps to the next calendar week when the account shows a specific delivery date.
2. Open the user's already authenticated meal-kit site. Treat browsing recipes, nutrition and current selections as read-only.
3. Collect every realistically selectable main meal before ranking. Record the displayed title, stable recipe identifier or recipe-card URL when available, calories per portion, protein, cook time, dietary labels, allergens, surcharge, availability, and whether it is already selected.
4. Use the account's current recipe details as authoritative for that delivery. Public recipe pages may help fill missing descriptions but must not override delivery-specific nutrition, ingredients, availability or price.
5. Apply all hard constraints from `preferences.yaml`. Exclude a meal when required data is missing and that missing value could violate a hard constraint. Explain shortages rather than silently relaxing a requirement.
6. Match candidates against `history.csv`. Prefer a stable recipe ID; otherwise compare normalized titles after removing presentation-only punctuation and common option prefixes such as `Double`.
7. Rank eligible meals using the configured preferences. Prioritize the longest time since last selected, then variety across proteins and cuisines, then soft preferences such as protein or cook time. Do not optimize one metric so aggressively that all selected meals become near-duplicates.
8. Return the proposed selection with calories, relevant dietary labels, last-selected date or `never`, any surcharge, and concise reasons. Clearly distinguish already-selected meals from proposed replacements.

When fewer eligible meals exist than requested, stop with a shortlist and identify which hard constraints caused the shortfall. Do not relax allergens or explicit exclusions. Suggest specific optional relaxations for the user to choose.

## Change an order

Planning or recommending meals does not authorize changing the live order.

Before the first action that adds, removes, replaces, continues, saves, or otherwise mutates the order, present the exact final selection and obtain explicit user approval. Treat the site's final continue/save/review control as a consequential external action and follow the active computer-use confirmation requirements.

After approval:

1. Change only the approved delivery and recipes.
2. Avoid optional add-ons, double-protein upgrades and premium surcharges unless they were explicitly approved.
3. Before saving, re-check meal count, servings, recipe names, surcharges, delivery date and edit deadline.
4. Save once. Reopen the delivery summary and verify that every approved meal is present with the expected serving count.
5. If verification differs from the approved plan, stop and report the discrepancy. Do not improvise replacements or repeatedly resubmit.

## Record history

Only record a plan after the site confirms it was saved, or when the user explicitly says they finalized it themselves. Append one row per confirmed recipe to `history.csv`; never rewrite older rows merely because a title changed.

Create a concise weekly report under `meal-planner/reports/YYYY-Www.md` when the user wants an audit trail. Include the delivery date, selection criteria, chosen recipes, key nutrition, replacements, and any approved constraint exception. Do not include account identifiers or session data.

Do not commit or push planner-file changes unless the user requests the Git action. Leave an accurate working-tree summary for a later commit workflow.

## Scheduled and unattended runs

For an unattended run, perform discovery, filtering and recommendation only. Produce the proposed plan and wait for approval before changing the live order. If the authenticated browser session, live menu, preference file, history file or required nutrition is unavailable, report the blocker without substituting unverified data.
