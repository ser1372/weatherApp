
<template>
  <p class="font-bold text-8xl text-center text-violet-400">
    Weather
    App
  </p>
  <div class="flex justify-center items-center">

    <div class="flex justify-center items-center flex-wrap w-[300px] h-[300px]">
      <input id="city" type="text"
        class="bg-purple-700  border-gray-300 text-gray-900 text-sm rounded-lgfocus:ring-blue-500 focus:border-blue-500 block w-full p-2.5  dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        placeholder="City" required>
      <button @click="sendCity()"
        class="text-white bg-purple-700 hover:bg-purple-800 focus:outline-none focus:ring-4 focus:ring-purple-300 font-medium rounded-full text-sm px-5 py-2.5 text-center mb-2 dark:bg-purple-600 dark:hover:bg-purple-700 dark:focus:ring-purple-900">
        Submit</button>
      <div id="currentWeather">
      </div>
    </div>

  </div>
</template>

<script setup>

function sendCity() {
  let city = document.getElementById('city').value;
  const apiKey = "9d59488c06cd2ec4de5b9c565d0478a8";

  const container = document.querySelector('#currentWeather');

  const requestGetParams = `q=${encodeURIComponent(city)}&units=metric&appid=${apiKey}`;
  const requestUrl = `https://api.openweathermap.org/data/2.5/weather?${requestGetParams}`;

  fetch(requestUrl).then(
    res => res.json()
  ).then(response => {
    const weatherDescriptions = response.weather.map(item => item.description);
    container.innerHTML = `<div><b>Main</b>: ${response.main.temp}</div>`
      + `<div><b>Description</b>: ${weatherDescriptions.join(', ')}</div>`;
  });

}
</script>


