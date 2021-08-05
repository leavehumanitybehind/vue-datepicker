<template>
  <div id="app">
    <div class="lang__wrapper">
      <button class="lang-btn lang-btn--ru" @click="currLang = 'ru'">ru</button>
      <button class="lang-btn lang-btn--en" @click="currLang = 'en'">en</button>
    </div>
    <DatePickerENG v-if="currLang === 'en'" />
    <DatePickerRU v-else />
  </div>
</template>

<script>
import DatePickerENG from "./components/DatePickerENG.vue";
import DatePickerRU from "./components/DatePickerRU.vue";
export default {
  components: { DatePickerENG, DatePickerRU },
  name: "App",
  data() {
    return {
      currLang: "en",
    };
  },
};
</script>
<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 40px;
  margin-left: auto;
  margin-right: auto;
}
.lang-btn:hover {
  background-color: rgba(128, 128, 128, 0.2);
}

.lang-btn--ru {
  border-right: 1px solid hsl(0, 0%, 80%);
}
</style>