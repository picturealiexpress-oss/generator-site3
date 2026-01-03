<!DOCTYPE html>
<html lang="uk">
<head>
<meta charset="UTF-8">
<title>Генератори / Інвертори</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body {font-family: Arial, sans-serif; margin:0; background:#f5f5f5;}
header {background:#111; color:#fff; padding:40px 20px; text-align:center;}
section {padding:20px; max-width:900px; margin:auto;}
.product {background:#fff; padding:20px; margin-bottom:20px; border-radius:8px;}
.product h3 {margin-top:0;}
.price {font-size:20px; font-weight:bold; color:#0a8f3c;}
button {
  background:#0a8f3c; color:#fff; border:none;
  padding:12px 20px; font-size:16px;
  cursor:pointer; border-radius:5px;
}
button:hover {opacity:0.9;}
form input, form textarea {
  width:100%; padding:10px; margin-bottom:10px;
  border-radius:4px; border:1px solid #ccc;
}
footer {text-align:center; padding:15px; font-size:14px; color:#666;}
</style>
</head>
<body>

<header>
  <h1>Генератори / Інвертори / Акумулятори</h1>
  <p>Ціни актуальні тільки для клієнтів. Замовлення онлайн.</p>
</header>

<section>

<div class="product">
  <h3>LiFePo4 зарядна станція Pecron 1800/1200 Вт</h3>
  <p>Портативна зарядна станція з LiFePO4 батареєю, до 10 пристроїв одночасно, бездротова зарядка. Ідеально для дому та виїздів.</p>
  <div class="price">18700 грн</div><br>
  <button onclick="setProduct('Pecron 1800/1200 Вт')">Замовити</button>
</div>

<div class="product">
  <h3>Комплект 5 кВт + 5.1 кВт·г Anenji + Datouboss</h3>
  <p>Інвертор Anenji 5 кВт з Wi-Fi модулем + акумулятор Datouboss LiFePO4 48V/100Ah для резервного живлення.</p>
  <div class="price">49900 грн</div><br>
  <button onclick="setProduct('Комплект 5 кВт + 5.1 кВт·г')">Замовити</button>
</div>

<div class="product">
  <h3>Акумулятор Datouboss LiFePO4 12V 100Ah</h3>
  <p>Літій-фосфатний акумулятор з BMS, 1280Wh. Надійний для інверторів та автономних систем.</p>
  <div class="price">9700 грн</div><br>
  <button onclick="setProduct('Datouboss 12V 100Ah')">Замовити</button>
</div>

<div class="product">
  <h3>Комплект 5 кВт + 10.2 кВт·г Anenji + 2 Datouboss</h3>
  <p>Потужний комплект резервного живлення з двома акумуляторами LiFePO4 48V/100Ah.</p>
  <div class="price">79900 грн</div><br>
  <button onclick="setProduct('Комплект 5 кВт + 10.2 кВт·г')">Замовити</button>
</div>

</section>

<section id="order">
<h2>Оформити замовлення</h2>

<form id="orderForm">
  <input type="hidden" id="product">
  <input type="text" id="name" placeholder="ПІБ отримувача" required>
  <input type="tel" id="phone" placeholder="Телефон" required>
  <input type="text" id="city" placeholder="Місто" required>
  <input type="text" id="np" placeholder="Відділення Нової Пошти" required>
  <textarea id="comment" placeholder="Коментар (необовʼязково)"></textarea>
  <button type="submit">Підтвердити замовлення</button>
</form>

<p id="status"></p>
</section>

<footer>
  Контакти: 0506403460 | Telegram: @gen697
</footer>

<script>
const TOKEN = "8086876554:AAGbv-Hr_HAbKfGfVKyh4VJUvDEr9-qcOzo";
const CHAT_ID = "@gen697";

function setProduct(name) {
  document.getElementById("product").value = name;
  document.getElementById("order").scrollIntoView({behavior:"smooth"});
}

document.getElementById("orderForm").addEventListener("submit", function(e){
  e.preventDefault();

  let text = `
📦 НОВЕ ЗАМОВЛЕННЯ

🛒 Товар: ${product.value}
👤 ПІБ: ${name.value}
📞 Телефон: ${phone.value}
🏙 Місто: ${city.value}
🏤 НП: ${np.value}
💬 Коментар: ${comment.value || "-"}
`;

  fetch(`https://api.telegram.org/bot${TOKEN}/sendMessage`, {
    method: "POST",
    headers: {"Content-Type":"application/json"},
    body: JSON.stringify({
      chat_id: CHAT_ID,
      text: text
    })
  })
  .then(()=>status.innerText="✅ Замовлення відправлено")
  .catch(()=>status.innerText="❌ Помилка відправки");
});
</script>

</body>
</html>
