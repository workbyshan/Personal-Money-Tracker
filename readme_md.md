# 💰 Personal Money Tracker

A lightweight, mobile-first personal finance web app engineered to require minimal input while automatically calculating balances, net worth, and receivables. Built as a single-file, zero-dependency application that runs entirely inside any mobile or desktop browser with full offline support.

---

## 🚀 Core Features

- **Automated Math & Balances**: Eliminates manual recalculation. Balance states update automatically on every entry.
- **True Net Worth Formula**:
  $$\text{Total Money} = \text{Bank 1} + \text{Bank 2} + \text{Cash} + \text{Money Given to Others}$$
  $$\text{Money Currently With Me} = \text{Bank 1} + \text{Bank 2} + \text{Cash}$$
- **Lent Money Treated as an Asset**: Money lent to friends or colleagues is tracked as an asset/receivable rather than an expense.
- **Overall Total Chart Widget**: Real-time interactive SVG donut chart displaying instant percentage distribution across all accounts.
- **Who Owes Me Drawer**: Dedicated debtor tracker with one-tap **Mark Returned** settlement.
- **Rollback Transaction History**: Chronological log with type filters (`Expense`, `Income`, `Lent`, `Returned`, `Transfer`) and a 1-tap delete button that rolls back balances without errors.
- **Zero Cloud / 100% Privacy**: All data is stored locally in the device's `localStorage`. Includes manual JSON export and restore options.
- **Mobile-First UX**: Dedicated keyboard buffers prevent the mobile soft-keyboard from obscuring inputs.

---

## 🛠️ Tech Stack

- **Markup & Logic**: HTML5, Vanilla JavaScript (ES6+)
- **Styling**: Tailwind CSS (via CDN)
- **Visuals**: Native SVG (No heavy third-party charting libraries)
- **Persistence**: Browser `localStorage` API

---

## 📥 Installation & Usage

### 1. Direct Browser Use
1. Download `personal_money_tracker.html`.
2. Open the file directly using Chrome, Safari, or any modern web browser.
3. No build step, node modules, or web servers required.

### 2. Install as Mobile App (PWA)
- **Android (Chrome)**: Tap the menu (⋮) $\rightarrow$ **Add to Home screen** / **Install app**.
- **iOS (Safari)**: Tap **Share** $\rightarrow$ **Add to Home Screen**.

---

## 💡 The Problem & How It Was Overcome

### 1. The "Lent Money Counted as an Expense" Flaw
- **The Problem**: Standard finance apps treat money lent to friends as spending or an expense. This falsely lowers your calculated net worth and causes confusion when the person eventually pays you back.
- **How It Was Overcome**: The app treats money lent as a balance transfer from a liquid account into an active receivable asset (`Money Given to Others`). Your liquid cash drops, but your total net worth remains unchanged until spent.

### 2. Mobile Keyboard Obscuring Form Inputs
- **The Problem**: On mobile screens, opening the virtual keyboard often hides active input fields and the submit button, forcing tedious manual scrolling.
- **How It Was Overcome**: Implemented an automated `scrollIntoView` focus listener combined with a `230px` keyboard buffer at the base of the viewport to keep the active typing field visible.

### 3. Accidental Overwrites and Math Errors
- **The Problem**: In manual ledger apps, editing or deleting an old entry often leaves balances out of sync, requiring manual recalculation.
- **How It Was Overcome**: An automated rollback mechanism ties directly into transaction IDs. Deleting a historical transaction automatically calculates and executes the exact inverse balance operation.

### 4. Heavy Chart Libraries Slowing Down Mobile Devices
- **The Problem**: Loading bloated charting packages (like Chart.js or D3.js) causes lag, external dependency failures, and slow initial rendering on mobile networks.
- **How It Was Overcome**: Built a custom, lightweight SVG donut chart using native `stroke-dasharray` and `stroke-dashoffset` calculations. It updates instantaneously with zero external dependencies.