---
name: Equinomy Mobile App — Feature & Architecture Snapshot
description: Complete feature map, screen inventory, and value propositions extracted from the equinomy-mobile codebase as of 2026-03-15.
type: project
---

Full codebase lives at `/mnt/c/dev/private/equinomy-frontend/equinomy-mobile/`.

**Why:** This memory exists so future feature-comparison scans can diff against this baseline rather than re-reading the entire codebase from scratch.

**How to apply:** On future scans, compare the current codebase against this snapshot to identify new, changed, or removed features. Only re-read files that are likely to have changed.

---

## Framework / Stack
- React Native 0.81.5 + Expo SDK ~54.0.33
- TypeScript (strict mode)
- React Navigation v7 (native stack + bottom tabs)
- Supabase (auth + database — no separate backend API)
- RevenueCat (`react-native-purchases`) for in-app subscriptions
- i18next — Swedish (default) and English
- expo-notifications for push notifications
- expo-image-picker for photo capture
- react-native-paper (Material Design UI)

---

## Navigation Structure

### Auth Flow (unauthenticated)
- Welcome → Auth → PhoneInput → OTPVerify / EmailAuth

### Onboarding Flow (new users)
- UserType → HorseDetails → EmptyState → MainTabs

### Main Tabs (5 tabs)
- Home (overview dashboard)
- Expenses (filterable/searchable list)
- AddExpense (add new expense form)
- Horses (horse roster)
- Statistics (charts and analytics)

### Stack Screens (from main tabs)
- Settings
- CategoryDetails
- PeriodPicker
- DateRangePicker
- HorseDetail
- HealthLog
- AddHealthEvent
- AddHealthSchedule
- ExpenseDetail
- ManageCategories

---

## All Features (as of 2026-03-15)

### Account & Onboarding
1. Multi-method authentication (Apple Sign-In, Google OAuth, email/password, phone/OTP)
2. User type selection at onboarding (horse owner, co-rider, riding school)
3. Guided first-horse setup during onboarding
4. Profile card with membership date in Settings

### Multi-Horse Management
5. Add/edit/delete unlimited horses (premium) or 1 horse (free)
6. Horse profiles: name, breed, birth date, stable, photo
7. Horse photo upload (camera or gallery)
8. Filter dashboard and charts by individual horse(s) or stable

### Expense Tracking
9. Add expenses: horse, category, type, amount, date, description
10. Edit and delete existing expenses
11. 12 built-in expense categories: Feed, Vet, Farrier, Training, Competition, Equipment, Horse Equipment, Rider Equipment, Boarding, Insurance, Transport, Other
12. Fixed vs. Spontaneous expense type tagging
13. Recurring expense flag with interval (daily/weekly/monthly/yearly)
14. Paginated, searchable expense list (sort by date or amount)

### AI Receipt Scanning (Premium / 3 free scans/month)
15. Scan receipts via camera or gallery
16. AI auto-fills amount, date, description, and category from receipt image
17. Free tier: 3 scans/month; unlimited with Premium

### Dashboard / Home
18. Donut chart showing expense breakdown by category for selected period
19. Period selector: weekly, monthly, yearly, last 7/30/90 days, custom date range
20. Navigate forward/backward through periods
21. Filter dashboard by horse(s) or stable
22. Category list with progress bars and amounts
23. Tap category to drill into CategoryDetails screen

### Statistics & Analytics
24. Period comparison card (current vs. prior equivalent period, absolute and % delta)
25. Monthly average and annual forecast KPI cards
26. Line chart — expense trend over time, with optional prior-period comparison overlay
27. Horizontal bar chart — expenses by category
28. Category comparison table (prior vs. current period with % change badges)
29. Seasonal heatmap — 12-month average spend pattern from 3 years of history
30. Fixed vs. Spontaneous split bar with percentage labels

### Budget Tracking (Premium)
31. Create budget items per category (monthly or yearly target)
32. Budget progress bars showing actual vs. target spend
33. Locked behind Premium paywall for free users

### Health Log (per horse)
34. Recurring health schedules: farrier, deworming, vaccination, dental, vet checkup, blood test, fecal test, other
35. Configurable interval (days/weeks/months) and next due date
36. Overdue / due soon / on-track status badges
37. Log a health event as done — automatically advances next due date
38. Optional reminder toggle with configurable days-before lead time
39. One-time health event logging with optional notes
40. Link health events to an expense record
41. Full event history per horse

### Push Notifications
42. Push notification registration on sign-in (Expo push token stored in profiles table)
43. Notifications enable/disable toggle in Settings
44. Notifications are used to remind users of upcoming/overdue health schedule events

### Custom Categories (Premium)
45. Create custom expense categories with a name and chosen color
46. Custom categories appear alongside built-in ones in expense forms and charts
47. Delete custom categories

### Settings
48. Language selector (Swedish / English) — persisted across sessions
49. Currency selector (SEK / EUR / GBP) — persisted to profile
50. Subscription management (upgrade, cancel, restore purchases)
51. In-app feedback form (bug report / feature request / other)
52. Privacy policy and Terms of Service links (language-aware)
53. Account deletion (calls Supabase edge function)
54. Sign out

### Subscription / Monetisation
55. Free tier: 1 horse, 3 receipt scans/month, no budget, no custom categories
56. Premium tier: unlimited horses, unlimited scans, budget tracking, custom categories
57. Monthly and annual plans via RevenueCat
58. force_premium flag in profiles table (grants free premium, e.g. to influencers)
59. Paywall modal is context-aware (horses / scanning / budget / general)
60. Restore purchases support (Apple/Google)

---

## Key Supabase Tables
horses, expenses, budget_items, receipt_scan_usage, feedback, profiles, health_events, health_schedules, custom_categories

## Key Supabase Edge Functions
- scan-receipt (AI receipt scanning)
- delete-account
- increment_receipt_scan (RPC)
