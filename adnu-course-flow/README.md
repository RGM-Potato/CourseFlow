# ADNU Course Flow — v2 (Supabase)

## Setup (do this once)

### 1. Create the Supabase tables

1. Go to your **Supabase Dashboard → SQL Editor → New Query**
2. Copy the contents of `schema.sql` and click **Run**
3. You should see 3 new tables: `courses`, `subjects`, `subject_prerequisites`

### 2. Add your credentials

Open `supabase.js` and fill in the two lines marked with 👈:

```js
const SUPABASE_URL = 'https://your-project-id.supabase.co'; // 👈
const SUPABASE_KEY = 'your-anon-public-key-here';           // 👈
```

Find these in: **Supabase Dashboard → Project Settings → API**

### 3. Install and run

```
npm install
npm start
```

Open **http://localhost:3000**

---

## How to use

- **Add a course** → click "+ Add a course" in the sidebar, fill in name/code, click **Save to Supabase**
- **View a course flow** → click any course in the sidebar
- **Add a subject** → select a course first, then click "+ Add subject" (top right)
- **View subject info** → click any subject pill → detail panel opens on the right
- **Prerequisite arrows** → drawn automatically between subjects in the same year view
- **Cross-year prerequisites** → shown as a `!` badge (hover it to see which subject)

---

## Database schema (summary)

| Table | Key columns |
|---|---|
| `courses` | id, name, code, color |
| `subjects` | id, course_id, code, name, units, category, description, instructor, year, semester |
| `subject_prerequisites` | subject_id, prerequisite_id |

---

## API reference

| Method | Route | Body | Purpose |
|---|---|---|---|
| GET | `/api/courses` | — | List all courses |
| GET | `/api/courses/:id` | — | Full course flow (years/semesters/subjects) |
| GET | `/api/subjects/:id` | — | Subject detail + resolved prerequisites |
| POST | `/api/courses` | `{ name, code, color }` | Add a course |
| POST | `/api/courses/:id/subjects` | `{ year, semester, code, name, units, category, instructor, description, prerequisiteCodes[] }` | Add a subject |
