<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>WeatherPeek</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #74ebd5, #ACB6E5);
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      margin: 0;
    }
    .container {
      text-align: center;
      background: rgba(255, 255, 255, 0.2);
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.2);
      width: 300px;
    }
    input {
      padding: 10px;
      border: none;
      border-radius: 8px;
      width: 70%;
    }
    button {
      padding: 10px;
      border: none;
      background: #0078D7;
      color: white;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover {
      background: #005fa3;
    }
    .weather-info {
      margin-top: 20px;
    }
    #weatherIcon {
      width: 80px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🌤️ WeatherPeek</h1>
    <div class="search-box">
      <input type="text" id="cityInput" placeholder="Enter city name" />
      <button id="searchBtn">Search</button>
    </div>
    <div class="weather-info">
      <h2 id="cityName">--</h2>
      <img id="weatherIcon" src="" alt="Weather Icon" />
      <p id="temperature">-- °C</p>
      <p id="description">--</p>
    </div>
  </div>

  <script>
    const apiKey = "";
    const searchBtn = document.getElementById("searchBtn");
    const cityInput = document.getElementById("cityInput");

    searchBtn.addEventListener("click", getWeather);

    function getWeather() {
      const cityName = cityInput.value.trim();
      if (!cityName) {
        alert("Please enter a city name");
        return;
      }

      fetch(`https://api.openweathermap.org/data/2.5/weather?q=${cityName}&appid=${apiKey}&units=metric`)
        .then(response => response.json())
        .then(data => {
          if (data.cod === "404") {
            alert("City not found!");
            return;
          }

          document.getElementById("cityName").textContent = data.name;
          document.getElementById("temperature").textContent = `${data.main.temp} °C`;
          document.getElementById("description").textContent = data.weather[0].description;
          document.getElementById("weatherIcon").src =
            `https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
        })
        .catch(() => {
          alert("Something went wrong. Please try again.");
        });
    }
  </script>
</body>
</html>
