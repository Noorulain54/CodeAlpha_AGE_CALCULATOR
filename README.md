# CodeAlpha_AGE_CALCULATOR
age calculator
# Age Calculator (HTML • CSS • JavaScript)

A simple, responsive web app that calculates a user’s exact age in **years, months, and days** from their **Date of Birth** using the JavaScript `Date` object.

---

## ✨ Features

* Input **Day / Month / Year**
* Calculates precise **Years, Months, Days**
* Handles month lengths & leap years
* Validates future dates & incomplete input
* Minimal, clean UI; mobile-friendly

---

## 🛠 Tech Stack

* **HTML** – structure
* **CSS** – styling
* **JavaScript** – age calculation with `Date`

---

## 🚀 Getting Started

1. **Create a file** named `index.html` and paste the code below.
2. **Open** `index.html` in any modern browser (double-click or drag into a browser window).

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Age Calculator</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f3f6fa; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
    .container { background: white; padding: 30px; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.2); text-align: center; width: 320px; }
    h2 { margin-bottom: 20px; color: #333; }
    .inputs { display:flex; gap:8px; justify-content:center; flex-wrap:wrap; }
    input { padding: 10px; border: 1px solid #ccc; border-radius: 6px; width: 90px; text-align: center; }
    button { margin-top: 15px; padding: 10px 20px; border: none; border-radius: 8px; background-color: #4CAF50; color: white; font-size: 16px; cursor: pointer; }
    button:hover { background-color: #45a049; }
    .result { margin-top: 20px; font-size: 18px; font-weight: bold; color: #222; min-height: 1.2em; }
  </style>
</head>
<body>
  <div class="container">
    <h2>Age Calculator</h2>
    <div class="inputs">
      <input type="number" id="day" placeholder="DD" min="1" max="31" aria-label="Day">
      <input type="number" id="month" placeholder="MM" min="1" max="12" aria-label="Month">
      <input type="number" id="year" placeholder="YYYY" min="1900" max="2100" aria-label="Year">
    </div>
    <button onclick="calculateAge()">Calculate</button>
    <div class="result" id="result" role="status" aria-live="polite"></div>
  </div>

  <script>
    function calculateAge() {
      const d = parseInt(document.getElementById('day').value, 10);
      const m = parseInt(document.getElementById('month').value, 10) - 1; // JS months: 0–11
      const y = parseInt(document.getElementById('year').value, 10);
      const resultEl = document.getElementById('result');

      if (Number.isNaN(d) || Number.isNaN(m) || Number.isNaN(y)) {
        resultEl.textContent = 'Please enter a complete Date of Birth.';
        return;
      }

      const dob = new Date(y, m, d);

      // Validate constructed date (e.g., Feb 31 -> invalid)
      if (dob.getFullYear() !== y || dob.getMonth() !== m || dob.getDate() !== d) {
        resultEl.textContent = 'Invalid date. Please check day, month, and year.';
        return;
      }

      const today = new Date();
      if (dob > today) {
        resultEl.textContent = 'DOB cannot be in the future.';
        return;
      }

      let years = today.getFullYear() - dob.getFullYear();
      let months = today.getMonth() - dob.getMonth();
      let days = today.getDate() - dob.getDate();

      if (days < 0) {
        months -= 1;
        // Days in previous month
        const prevMonth = new Date(today.getFullYear(), today.getMonth(), 0);
        days += prevMonth.getDate();
      }

      if (months < 0) {
        years -= 1;
        months += 12;
      }

      resultEl.textContent = `You are ${years} Years, ${months} Months, and ${days} Days old.`;
    }
  </script>
</body>
</html>
```

---

## 📁 Suggested Project Structure

```
age-calculator/
└── index.html
```

> For larger projects, split CSS/JS into `styles.css` and `script.js`.

---

## 🧠 How the Calculation Works

* Compute a provisional difference of **years / months / days** between **today** and **DOB**.
* If **days < 0**, borrow days from the previous month (auto-handles month length & leap years).
* If **months < 0**, borrow 12 months and reduce years by 1.

---

## ✅ Validation & Edge Cases

* **Incomplete input** → prompts user to complete date
* **Invalid date** (e.g., 31/02/2000) → shows an error
* **Future DOB** → blocked with a clear message

---

## 📱 Accessibility & Responsiveness

* Inputs have **ARIA labels**; result uses `aria-live` for screen readers.
* Flex layout adapts to narrow screens.

---

## 🌐 Browser Support

Works in all modern browsers (Chrome, Edge, Firefox, Safari). No build tools required.

---

## 🧩 Customization Tips

* Change theme colors in the `<style>` block.
* Replace inline styles with separate CSS file for maintainability.
* Add keyboard handling or auto-jump between inputs (optional).

---

## 🔧 Troubleshooting

* **Blank result**: Ensure all three fields are filled with numbers.
* **Wrong age**: Verify system date/time and input order (DD/MM/YYYY).

---

## 📄 License

MIT — free to use, modify, and share.

---

## 🙌 Credits

Made by *Your Name*. Inspired by beginner-friendly JS date utilities.

