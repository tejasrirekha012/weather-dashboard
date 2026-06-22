<!DOCTYPE html>
<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Weather Dashboard</title>

<link rel="stylesheet" href="style.css">

</head>

<body>

<div class="container">

<h1>Weather Dashboard</h1>

<div class="search-box">

<input
type="text"
id="city"
placeholder="Enter city name"
>

<button id="searchBtn">

Search

</button>

</div>

<div id="weather">

<p>Search a city to view weather.</p>

</div>

</div>

<script src="script.js"></script>

</body>
</html>
const cityInput = document.getElementById("city");

const searchBtn = document.getElementById("searchBtn");

const weatherDiv = document.getElementById("weather");

searchBtn.addEventListener("click", getWeather);

async function getWeather() {

  const city = cityInput.value.trim();

  if (!city) {

    weatherDiv.innerHTML = "<p>Please enter a city name.</p>";

    return;

  }

  weatherDiv.innerHTML = "<p>Loading...</p>";

  try {

    const response = await fetch(

      `https://wttr.in/${encodeURIComponent(city)}?format=j1`

    );

    if (!response.ok) {

      throw new Error("Unable to fetch weather");

    }

    const data = await response.json();

    const current = data.current_condition[0];

    weatherDiv.innerHTML = `

      <div class="weather-card">

        <h2>${city.toUpperCase()}</h2>

        <p>🌡️ Temperature: ${current.temp_C} °C</p>

        <p>💧 Humidity: ${current.humidity}%</p>

        <p>🌬️ Wind Speed: ${current.windspeedKmph} km/h</p>

        <p>☁️ Condition: ${current.weatherDesc[0].value}</p>

      </div>

    `;

  }

  catch(error) {

    weatherDiv.innerHTML = `

      <p class="error">

      ${error.message}

      </p>

    `;

  }

}
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Arial,sans-serif;
}

body{

display:flex;

justify-content:center;

align-items:center;

min-height:100vh;

background:#f4f4f4;
}

.container{

width:400px;

background:white;

padding:30px;

border-radius:15px;

box-shadow:0 0 15px rgba(0,0,0,0.2);

text-align:center;
}

h1{

margin-bottom:20px;
}

.search-box{

display:flex;

gap:10px;

margin-bottom:25px;
}

input{

flex:1;

padding:10px;

font-size:16px;

border:1px solid #ccc;

border-radius:8px;
}

button{

padding:10px 20px;

border:none;

background:#007bff;

color:white;

cursor:pointer;

border-radius:8px;
}

button:hover{

background:#0056b3;
}

.weather-card{

line-height:2;
}

.error{

color:red;

font-weight:bold;
}
