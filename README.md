# 📚 Class Timetable (Svelte)

A simple **Svelte+Vite based timetable viewer** for a class in school.  
This project fetches YAML data from a remote JSON API, parses it, and renders a weekly schedule with clickable period cells.

---

## 🚀 Features
- Fetches timetable data from a hosted JSON API (`jsonhosting.com`).
- Parses YAML content into a JavaScript object using [`yaml`](https://www.npmjs.com/package/yaml).
- Displays **full-week** or **single-day** schedules.
- Modular components:
  - `DaySelector.svelte` → dropdown for selecting day/full-week.
  - `PeriodCell.svelte` → renders each period cell (clickable).
- **Clickable cells**: entire period cell opens the Google Meet link in a new tab.
- Hover effects: pointer cursor + background highlight.
- Lunch periods styled differently for clarity.

---

## 🛠️ Tech Stack
- **Frontend Framework**: [Svelte](https://svelte.dev/)
- **Data Parsing**: [yaml](https://www.npmjs.com/package/yaml)
- **Styling**: Vanilla CSS (scoped in components)

---

## 📂 Project Structure
```
src/
 ├── App.svelte              # Main entry point
 ├── lib/TimeTable.svelte    # Main timetable component
 ├── lib/DaySelector.svelte  # Dropdown for day selection
 ├── lib/PeriodCell.svelte   # Individual period cell
 └── main.js                 # Svelte bootstrap
```

---

## ⚙️ Setup & Installation

1. **Clone the repo**
   ```bash
   git clone https://github.com/isurfer21/class-timetable.git
   cd class-timetable
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Run the dev server**
   ```bash
   npm run dev
   ```

4. Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## 📖 Usage

- On load, the app fetches timetable data from public assets.
- The JSON response contains timetable data in YAML format.
- The YAML is parsed into `timeTableData` and rendered.

### Example YAML:
```yaml
class_name: CLASS 1 PURPLE
time_slots:
  Yoga: "8:30-8:50"
  Assembly: "8:55-9:05"
  P1: "9:10-9:40"
schedule:
  MONDAY:
    Yoga:
      subject: Yoga
      teacher: CT
      meet_link: https://meet.google.com/qwt-domp-jgg
```

---

## 🎨 Styling
- **Clickable cells**: green hover highlight, pointer cursor.
- **Lunch cells**: red background, bold text.
- **Day headers**: purple background with white text.

---

## 🧩 Components

### `DaySelector.svelte`
- Renders a dropdown with options: `Full Week`, `MONDAY`, `TUESDAY`, etc.
- Uses `bind:value` to update `selectedDay`.

### `PeriodCell.svelte`
- Renders subject, teacher, classroom code.
- Entire cell is clickable if `meet_link` exists.
- Hover effect highlights the cell.

---

## 🧪 Testing
- Verify timetable loads correctly from API.
- Check that clicking a period cell opens the correct Google Meet link.
- Ensure hover styles apply consistently.

---

## 📌 Future Improvements
- Add loading/error states for fetch.
- Support multiple classes via config.
- Export timetable to PDF/Excel.
- Add responsive design for mobile.