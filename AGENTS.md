# Project Memory & Architecture: Expense Tracker

## Project Overview
- **Name:** Expense Tracker / Finance Tracker
- **Type:** Single Page Application (SPA)
- **Tech Stack:** React 19, Vite, Plain CSS, ESLint
- **Course Starter:** Code With Mosh (Course Starter)

---

## Directory & File Structure

```
expense-tracker-starter/
├── index.html              # HTML entry point (Mounts #root)
├── package.json            # Scripts & dependencies (React 19, Vite)
├── vite.config.js          # Vite config with React plugin
├── eslint.config.js        # ESLint flat config
├── public/                 # Static assets (Vite svg)
└── src/
    ├── main.jsx            # React root mount point (StrictMode)
    ├── App.jsx             # Main application component containing all state & UI
    ├── App.css             # Component-specific styles (summary cards, form, table, delete-btn)
    └── index.css           # Global reset & base styles
```

---

## Architecture & State Management

Currently, the entire application state is managed inside [`src/App.jsx`](src/App.jsx):

### Data Schema
- **Transaction Object:**
  ```typescript
  {
    id: number,          // Unique identifier (timestamp or integer)
    description: string, // Item description
    amount: string,      // Transaction amount (stored as string / converted for math)
    type: "income" | "expense",
    category: "food" | "housing" | "utilities" | "transport" | "entertainment" | "salary" | "other",
    date: string         // YYYY-MM-DD format
  }
  ```

### State Variables in `App.jsx`
- `transactions`: Array of transaction items.
- `description`, `amount`, `type`, `category`: Controlled input states for the "Add Transaction" form.
- `filterType`: Filter for all / income / expense.
- `filterCategory`: Filter for all / specific categories.

### Derived Computations
- `totalIncome`: Sum of all `income` transactions.
- `totalExpenses`: Sum of all `expense` transactions.
- `balance`: `totalIncome - totalExpenses`.
- `filteredTransactions`: Filtered view based on `filterType` and `filterCategory`.

---

## Key Functions & Handlers

- **`handleSubmit(e)`**: Validates form inputs, creates a new transaction with a timestamp ID and current date, appends it to `transactions`, and resets form state.
- **`handleDeleteTransaction(id)`**: Triggers a confirmation dialog (`window.confirm`) and removes the transaction with matching `id` from state via `filter()`.

---

## Styling & Classes (`src/App.css`)

- `.app`: Centered container (`max-width: 800px`).
- `.summary` / `.summary-card`: Flexbox cards displaying Income, Expenses, Balance.
- `.income-amount` / `.expense-amount`: Green / red amounts.
- `.add-transaction`: Form box with responsive wrap.
- `table`: Full-width data table with `.delete-btn` for removing items.

---

## Development Workflow & Commands

```bash
# Start development server at http://localhost:5173
npm run dev

# Create production build
npm run build

# Run linter
npm run lint

# Preview production build
npm run preview
```

---

## Conventions & Best Practices
- **Component Handlers:** Prefix internal handlers with `handle` (e.g., `handleSubmit`, `handleDeleteTransaction`).
- **Props (if extracting subcomponents):** Use `on*` for event callback props (e.g., `onDeleteTransaction`, `onAddTransaction`).
- **State Immutability:** Always use immutable updates (`setTransactions([...transactions, newItem])` or `filter()`).

