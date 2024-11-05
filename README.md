# tsag_agaar<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Information</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: Arial, sans-serif;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            background: linear-gradient(to bottom right, #4facfe, #00f2fe);
            color: #333;
        }

        .container {
            text-align: center;
            padding: 20px;
            width: 100%;
            max-width: 400px;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
        }

        h1 {
            font-size: 24px;
            color: #333;
            margin-bottom: 20px;
        }

        .input-group {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
        }

        #city-input {
            padding: 10px;
            width: 70%;
            border: 1px solid #ddd;
            border-radius: 5px;
            outline: none;
            font-size: 16px;
        }

        button {
            padding: 10px 15px;
            font-size: 16px;
            color: white;
            background-color: #ff4500;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #e03e00;
        }

        .weather-container {
            background-color: #fff;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }

        .temperature {
            font-size: 48px;
            color: #ff4500;
            margin: 15px 0;
        }

        .description {
            font-size: 20px;
            text-transform: capitalize;
            color: #333;
            margin-bottom: 10px;
        }

        .info p {
            font-size: 16px;
            color: #555;
        }
    </style>
</head>

<body>
    <div class="container">
        <h1>Weather Information</h1>

        <div class="input-group">
            <input type="text" id="city-input" placeholder="Enter city name" />
            <button onclick="fetchWeather()">Get Weather</button>
        </div>

        <div class="weather-container" id="weather">
            <p>Enter a city to see the weather.</p>
        </div>
    </div>

    <script>
        const apiKey = 'a45bbe72345d8eef11b88a31e3933d0f';

        async function fetchWeather() {
            const city = document.getElementById('city-input').value || 'Ulaanbaatar';
            try {
                const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${apiKey}`);
                const data = await response.json();

                if (data.cod === 200) {
                    document.getElementById('weather').innerHTML = `
                        <div class="temperature">${data.main.temp}°C</div>
                        <div class="description">${data.weather[0].description}</div>
                        <div class="info">
                            <p>Humidity: ${data.main.humidity}%</p>
                            <p>Wind Speed: ${data.wind.speed} m/s</p>
                            <p>Feels Like: ${data.main.feels_like}°C</p>
                        </div>
                    `;
                } else {
                    document.getElementById('weather').innerHTML = `<p>${data.message}</p>`;
                }
            } catch (error) {
                document.getElementById('weather').innerHTML = `<p>Error fetching weather data.</p>`;
            }
        }
    </script>
</body>

</html>
