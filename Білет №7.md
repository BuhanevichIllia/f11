<!-- Сайт розроблено студентом Іллею Буханевичом, група ФІТ2-11 -->
<!DOCTYPE html>
<html lang="uk">
<head>
  <meta charset="UTF-8">
  <title>Сервіс доставки</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #005c99;
      color: white;
      padding: 15px;
      text-align: center;
    }
    nav ul {
      list-style: none;
      padding: 0;
      display: flex;
      justify-content: center;
      gap: 20px;
    }
    nav a {
      color: white;
      text-decoration: none;
      font-weight: bold;
    }
    main {
      padding: 20px;
    }
    .section {
      display: none;
    }
    .section.active {
      display: block;
    }
    label {
      display: block;
      margin: 10px 0 5px;
    }
    input, select, button {
      padding: 5px;
      width: 100%;
      max-width: 300px;
      margin-bottom: 10px;
    }
    button {
      cursor: pointer;
      background-color: #005c99;
      color: white;
      border: none;
    }
    .result {
      margin-top: 10px;
      font-weight: bold;
    }
    footer {
      background-color: #f0f0f0;
      padding: 10px;
      text-align: center;
      font-size: 0.9em;
      border-top: 1px solid #ccc;
    }
  </style>
</head>
<body>
  <header>
    <h1>Сервіс доставки</h1>
    <nav>
      <ul>
        <li><a href="#" onclick="showSection('home')">Головна</a></li>
        <li><a href="#" onclick="showSection('calculator')">Калькулятор</a></li>
        <li><a href="#" onclick="showSection('about')">Про нас</a></li>
      </ul>
    </nav>
  </header>

  <main>
    <section id="home" class="section active">
      <h2>Ласкаво просимо</h2>
      <p>Вас вітає сервіс доставки. Перейдіть у розділ калькулятора, щоб розрахувати вартість.</p>
    </section>

    <section id="calculator" class="section">
      <h2>Калькулятор доставки</h2>
      <label for="city">Місто:</label>
      <select id="city"></select>

      <label for="weight">Вага (кг):</label>
      <input type="number" id="weight" min="0.1" step="0.1" placeholder="Наприклад: 2.5">

      <label for="type">Тип доставки:</label>
      <select id="type">
        <option value="standard">Стандартна</option>
        <option value="express">Експрес</option>
      </select>

      <button onclick="calculate()">Розрахувати</button>

      <div class="result" id="result"></div>
    </section>

    <section id="about" class="section">
      <h2>Про нас</h2>
      <p>Цей сайт розроблено в рамках навчального проєкту.<br>Автор: Ілля Буханевич, група ФІТ-2-11.</p>
    </section>
  </main>

  <footer>
    <p>© 2025 Ілля Буханевич, група ФІТ-2-11</p>
  </footer>

  <script>
    // Сайт розроблено студентом Іллею Буханевичом, група ФІТ2-11

    const cities = [
      { name: "Київ", value: "kyiv", rate: 20 },
      { name: "Львів", value: "lviv", rate: 25 },
      { name: "Одеса", value: "odesa", rate: 30 }
    ];

    function populateCities() {
      const citySelect = document.getElementById("city");
      cities.forEach(city => {
        const option = document.createElement("option");
        option.value = city.value;
        option.textContent = city.name;
        citySelect.appendChild(option);
      });
    }

    function showSection(id) {
      const sections = document.querySelectorAll('.section');
      sections.forEach(section => {
        section.classList.remove('active');
      });
      document.getElementById(id).classList.add('active');
    }

    function calculate() {
      const cityValue = document.getElementById("city").value;
      const weight = parseFloat(document.getElementById("weight").value);
      const type = document.getElementById("type").value;

      if (!weight || weight <= 0) {
        document.getElementById("result").innerText = "Введіть коректну вагу.";
        return;
      }

      const city = cities.find(c => c.value === cityValue);
      if (!city) {
        document.getElementById("result").innerText = "Невідоме місто.";
        return;
      }

      const multiplier = type === "express" ? 1.5 : 1;
      const cost = (city.rate + weight * 10) * multiplier;

      document.getElementById("result").innerText = `Вартість доставки: ${cost.toFixed(2)} грн`;
    }

    // Ініціалізація при завантаженні сторінки
    window.onload = populateCities;
  </script>
</body>
</html>
