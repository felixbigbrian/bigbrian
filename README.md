# bigbrian
Testing 
<form id="search-form" class="search">
  <input type="text" id="city-input" placeholder="Enter city (e.g., London)" required>
  <button type="submit">Search</button>
</form>

<section id="current" class="card hidden">
  <h2 id="current-city"></h2>
  <div class="current-row">
    <div class="current-main">
      <img id="current-icon" alt="" />
      <div>
        <div id="current-temp" class="temp"></div>
        <div id="current-desc" class="desc"></div>
      </div>
    </div>
    <ul class="current-details">
      <li>Feels like: <span id="current-feels"></span></li>
      <li>Humidity: <span id="current-humidity"></span></li>
      <li>Wind: <span id="current-wind"></span></li>
    </ul>
  </div>
</section>

<section id="forecast" class="hidden">
  <h3>3-Day Forecast</h3>
  <div id="forecast-cards" class="forecast-grid"></div>
</section>

<div id="error" class="error hidden"></div>

<footer>
  <small>Data from OpenWeatherMap | Demo site</small>
</footer>
</main>

<script src="script.js"></script>

</body>

</html>

:root{
--bg:#f4f7fb;
--card:#ffffff;
--accent:#1e88e5;
--muted:#6b7280;
--max-width:800px;
}

*{box-sizing:border-box}
html,body{height:100%}
body{
margin:0;
font-family:system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;
background:linear-gradient(180deg,var(--bg),#eef3fb);
color:#111827;
display:flex;
align-items:flex-start;
justify-content:center;
padding:32px 16px;
}

.container{
width:100%;
max-width:var(--max-width);
background:transparent;
}

h1{margin:0 0 12px;font-size:1.6rem}
h2{margin:0 0 8px}
.card{
background:var(--card);
border-radius:12px;
padding:16px;
box-shadow:0 6px 18px rgba(16,24,40,0.06);
margin:12px 0;
}

.search{display:flex;gap:8px;margin-bottom:8px}
.search input{
flex:1;padding:10px 12px;border-radius:8px;border:1px solid #e6eef7;background:white;
}
.search button{
padding:10px 12px;border-radius:8px;border:0;background:var(--accent);color:white;font-weight:600;
cursor:pointer;
}
.search button:active{transform:translateY(1px)}

.current-row{display:flex;flex-direction:column;gap:12px}
.current-main{display:flex;align-items:center;gap:12px}
.current-main img{width:80px;height:80px}
.temp{font-size:1.6rem;font-weight:700}
.desc{color:var(--muted);text-transform:capitalize}
.current-details{list-style:none;padding:0;margin:0;color:var(--muted)}
.current-details li{margin:6px 0}

.forecast-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:12px;margin-top:8px}
.forecast-card{
background:linear-gradient(180deg,#fff,#fbfdff);
border-radius:10px;padding:10px;text-align:center;border:1px solid #eef6ff;
}
.forecast-card img{width:48px;height:48px}
.forecast-card .day{font-weight:600;margin-top:6px}
.forecast-card .range{color:var(--muted);margin-top:4px}

.error{
margin-top:12px;padding:10px;border-radius:8px;background:#fff0f0;color:#7f1d1d;border:1px solid #ffd1d1;
}

.hidden{display:none}

footer{margin-top:18px;color:var(--muted);font-size:0.9rem}

@media (min-width:640px){
.current-row{flex-direction:row;justify-content:space-between;align-items:center}
}
const API_KEY = "YOUR_API_KEY_HERE"; // <-- put your key here

const $ = sel => document.querySelector(sel);
const form = $('#search-form');
const cityInput = $('#city-input');
const errorEl = $('#error');
const currentSection = $('#current');
const forecastSection = $('#forecast');
const currentCity = $('#current-city');
const currentIcon = $('#current-icon');
const currentTemp = $('#current-temp');
const currentDesc = $('#current-desc');
const currentFeels = $('#current-feels');
const currentHumidity = $('#current-humidity');
const currentWind = $('#current-wind');
const forecastCards = $('#forecast-cards');

form.addEventListener('submit', e => {
e.preventDefault();
const city = cityInput.value.trim();
if (!city) return;
fetchWeatherByCity(city);
});

async function fetchWeatherByCity(city){
clearUI();
try{
// Use OpenWeatherMap Geocoding API to get lat/lon from city name
const geoRes = await fetch(https://api.openweathermap.org/geo/1.0/direct?q=${encodeURIComponent(city)}&limit=1&appid=${API_KEY});
if (!geoRes.ok) throw new Error('Geocoding failed');
const geo = await geoRes.json();
if (!geo || geo.length === 0) {
showError('City not found. Try a different name.');
return;
}
const { lat, lon, name, country, state } = geo[0];

// Use One Call (v3) / or One Call (v2) for current + daily forecast
// We'll use the One Call v1 "onecall" endpoint (works with API key)
// Note: OpenWeather changed its API versions; this example uses the onecall endpoint for simplicity.
const weatherRes = await fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=${lat}&lon=${lon}&units=metric&exclude=minutely,hourly,alerts&appid=${API_KEY}`);
if (!weatherRes.ok) throw new Error('Weather fetch failed');
const data = await weatherRes.json();

renderCurrent({ name, country, state, current: data.current });
renderForecast(data.daily);
} catch (err) {
console.error(err);
showError('Unable to fetch weather. Check your network and API key.');
}
}

function renderCurrent({ name, country, state, current }){
const displayName = state ? ${name}, ${state}, ${country} : ${name}, ${country};
currentCity.textContent = displayName;
const icon = current.weather && current.weather[0] ? current.weather[0].icon : '01d';
currentIcon.src = https://openweathermap.org/img/wn/${icon}@2x.png;
currentIcon.alt = current.weather && current.weather[0] ? current.weather[0].description : 'weather';
currentTemp.textContent = ${Math.round(current.temp)}°C;
currentDesc.textContent = current.weather && current.weather[0] ? current.weather[0].description : '';
currentFeels.textContent = ${Math.round(current.feels_like)}°C;
currentHumidity.textContent = ${current.humidity}%;
currentWind.textContent = ${(current.wind_speed || 0)} m/s;
currentSection.classList.remove('hidden');
}

function renderForecast(daily){
// daily[0] is today; show days 1..3 (next 3 days)
forecastCards.innerHTML = '';
for (let i = 1; i <= 3 && i < daily.length; i++){
const day = daily[i];
const date = new Date(day.dt * 1000);
const dayName = date.toLocaleDateString(undefined, { weekday: 'short' });
const icon = day.weather && day.weather[0] ? day.weather[0].icon : '01d';
const desc = day.weather && day.weather[0] ? day.weather[0].description : '';
const max = Math.round(day.temp.max);
const min = Math.round(day.temp.min);
const card = document.createElement('div');
card.className = 'forecast-card card';
card.innerHTML = `
  <img src="https://openweathermap.org/img/wn/${icon}@2x.png" alt="${desc}">
  <div class="day">${dayName}</div>
  <div class="range">${max}° / ${min}°</div>
  <div class="desc" style="margin-top:6px;color:var(--muted);text-transform:capitalize">${desc}</div>
`;
forecastCards.appendChild(card);
}
forecastSection.classList.remove('hidden');
}

function showError(msg){
errorEl.textContent = msg;
errorEl.classList.remove('hidden');
}

function clearUI(){
errorEl.classList.add('hidden');
currentSection.classList.add('hidden');
forecastSection.classList.add('hidden');
forecastCards.innerHTML = '';
}
