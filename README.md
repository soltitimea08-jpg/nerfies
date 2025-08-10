<!DOCTYPE html>
<html lang="hu">
<head>
<meta charset="UTF-8">
<title>Hova tettem?</title>
<style>
  body { font-family: Arial, sans-serif; background: #f0f0f0; margin: 0; padding: 20px; }
  h1 { color: #333; }
  .container { background: white; padding: 20px; border-radius: 10px; max-width: 500px; margin: auto; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
  input, button { width: 100%; padding: 10px; margin: 5px 0; font-size: 16px; }
  .list { margin-top: 20px; }
  .item { padding: 10px; background: #fafafa; border-bottom: 1px solid #ddd; }
</style>
</head>
<body>
<div class="container">
  <h1>📦 Hova tettem?</h1>
  <input id="item" placeholder="Tárgy neve (pl. kézi fúró)">
  <input id="location" placeholder="Hely (pl. garázs - 2. polc)">
  <button onclick="saveItem()">Mentés</button>
  <hr>
  <input id="search" placeholder="Mit keresel?">
  <button onclick="findItem()">Keresés</button>
  <div class="list" id="results"></div>
</div>

<script>
function saveItem() {
    let item = document.getElementById("item").value.trim();
    let location = document.getElementById("location").value.trim();
    if (!item || !location) { alert("Adj meg tárgyat és helyet!"); return; }
    let data = JSON.parse(localStorage.getItem("memory") || "[]");
    data.push({item, location, time: new Date().toLocaleString()});
    localStorage.setItem("memory", JSON.stringify(data));
    alert("Elmentve!");
    document.getElementById("item").value = "";
    document.getElementById("location").value = "";
}

function findItem() {
    let search = document.getElementById("search").value.trim().toLowerCase();
    let data = JSON.parse(localStorage.getItem("memory") || "[]");
    let results = data.filter(d => d.item.toLowerCase().includes(search));
    let out = "";
    if (results.length === 0) out = "<p>Nincs találat.</p>";
    else results.reverse().forEach(r => {
        out += `<div class="item"><b>${r.item}</b> → ${r.location} <br><small>${r.time}</small></div>`;
    });
    document.getElementById("results").innerHTML = out;
}
</script>
</body>
</html>
