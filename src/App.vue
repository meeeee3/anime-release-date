<template>
  <div>
    <h1>Anime Weekly Schedule</h1>
    <table>
      <thead>
        <tr>
          <th>Monday</th>
          <th>Tuesday</th>
          <th>Wednesday</th>
          <th>Thursday</th>
          <th>Friday</th>
          <th>Saturday</th>
          <th>Sunday</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td v-for="(animeList, day) in weeklyAnime" :key="day" :class="{ highlight: isToday(day) }">
            <ul>
              <li v-for="anime in animeList" :key="anime.title">
                <a :href="anime.link" target="_blank">{{ anime.title }}</a>
              </li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// 將動畫資料直接嵌入到程式碼中
const weeklyAnime = ref({
  "Monday": [
    {"title": "Attack on Titan", "link": "https://example.com/attack-on-titan"},
    {"title": "Spy x Family", "link": "https://example.com/spy-x-family"}
  ],
  "Tuesday": [
    {"title": "One Piece", "link": "https://example.com/one-piece"}
  ],
  "Wednesday": [
    {"title": "Naruto", "link": "https://example.com/naruto"},
    {"title": "Bleach", "link": "https://example.com/bleach"}
  ],
  "Thursday": [
    {"title": "My Hero Academia", "link": "https://example.com/my-hero-academia"}
  ],
  "Friday": [
    {"title": "Demon Slayer", "link": "https://example.com/demon-slayer"}
  ],
  "Saturday": [
    {"title": "Jujutsu Kaisen", "link": "https://example.com/jujutsu-kaisen"},
    {"title": "Tokyo Revengers", "link": "https://example.com/tokyo-revengers"}
  ],
  "Sunday": [
    {"title": "Black Clover", "link": "https://example.com/black-clover"}
  ]
});

const daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
const today = ref('');

// 獲取當前日期是星期幾
const getToday = () => {
  const currentDayIndex = new Date().getDay();
  today.value = daysOfWeek[currentDayIndex];
};

// 檢查是否是當天放映的動畫
const isToday = (day) => {
  return day === today.value;
};

// 在組件掛載後獲取當前星期
onMounted(() => {
  getToday();
});

export default {
  name: "App",
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid black;
  padding: 10px;
  text-align: center;
}

.highlight {
  background-color: yellow;
}
</style>
