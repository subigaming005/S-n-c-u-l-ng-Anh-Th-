# Sân cầu lông anh thư
<!DOCTYPE html><html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Tính tiền sân cầu lông</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; max-width: 600px; margin: auto; }
    label, select, input, button { display: block; margin: 10px 0; width: 100%; }
    .checkbox-list label { display: flex; justify-content: space-between; }
  </style>
</head>
<body>
  <h2>Tính tiền sân cầu lông</h2><label>Giờ bắt đầu: <input type="time" id="startTime"></label> <label>Giờ kết thúc: <input type="time" id="endTime"></label>

  <h3>Nước giải khát</h3>
  <div class="checkbox-list" id="drinkList"></div>  <h3>Đồ ăn</h3>
  <div class="checkbox-list" id="foodList"></div><button onclick="calculateTotal()">Tính tổng tiền</button>

  <h3 id="result">Tổng tiền: 0 ₫</h3>  <script>
    const hourlyRate = 60000;
    const drinks = {
      "Nước suối": 5000,
      "C2 đào": 10000,
      "Trà xanh": 10000,
      "Pocari": 15000,
      "Trà đá (loại 1)": 10000,
      "Trà đá (loại 2)": 5000,
      "Revive": 10000
    };

    const foods = {
      "Mì xào 1 gói 1 trứng": 15000,
      "Mì xào 2 gói 1 trứng": 20000,
      "Mì xào 2 gói 2 trứng": 25000,
      "Mì xào 3 gói 1 trứng": 30000
    };

    const drinkList = document.getElementById('drinkList');
    const foodList = document.getElementById('foodList');

    for (const [name, price] of Object.entries(drinks)) {
      drinkList.innerHTML += `<label><span>${name} (${price.toLocaleString()}₫)</span><input type='checkbox' value='${price}'></label>`;
    }

    for (const [name, price] of Object.entries(foods)) {
      foodList.innerHTML += `<label><span>${name} (${price.toLocaleString()}₫)</span><input type='checkbox' value='${price}'></label>`;
    }

    function calculateTotal() {
      const start = document.getElementById("startTime").value;
      const end = document.getElementById("endTime").value;
      let total = 0;

      if (start && end) {
        const [h1, m1] = start.split(":").map(Number);
        const [h2, m2] = end.split(":").map(Number);
        const startMinutes = h1 * 60 + m1;
        const endMinutes = h2 * 60 + m2;
        const durationHours = (endMinutes - startMinutes) / 60;
        if (durationHours > 0) total += durationHours * hourlyRate;
      }

      drinkList.querySelectorAll("input:checked").forEach(input => total += Number(input.value));
      foodList.querySelectorAll("input:checked").forEach(input => total += Number(input.value));

      document.getElementById("result").innerText = `Tổng tiền: ${total.toLocaleString()} ₫`;
    }
  </script></body>
</html>
