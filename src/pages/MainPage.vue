<template>
  <div class="container">
    <button class="btn-switch btn-reset"
    @click="changeLang">
      {{ switchText }}
    </button>

    <CalendarRu v-if="isLangRus"
    :days="getCalendarDays"
    :current-day="currentDay"/>

    <CalendarEng v-else
    :days="getCalendarDays"
    :current-day="currentDay"/>
  </div>
</template>

<script setup>
import { ref, computed, provide } from 'vue';
import CalendarRu from '@/components/CalendarRu.vue';
import CalendarEng from '@/components/CalendarEng.vue';

const date = ref(new Date());
const currentYear = ref(date.value.getFullYear());
const currentMonth = ref(date.value.getMonth());
const currentDay = ref(date.value.getDate());
const isLangRus = ref(true);
const switchText = ref('Сменить язык');

const getCalendarDays = computed(() => {
  const result = [];
  const month = currentMonth.value;
  const firstDayMonth = new Date(currentYear.value, currentMonth.value, 1);

  firstDayMonth.setDate(firstDayMonth.getDate() - (((firstDayMonth.getDay() || 7) - 1) || 7));

  for (let i = 0; i < 42; i += 1, firstDayMonth.setDate(firstDayMonth.getDate() + 1)) {
    result.push({
      date: firstDayMonth.getDate(),
      currentMonth: firstDayMonth.getMonth() === month,
      id: Math.random(3000),
    });
  }

  return result;
});

const changeMonth = (step) => {
  date.value = new Date(date.value.setMonth(date.value.getMonth() + step));
};

const changeLang = () => {
  if (isLangRus.value) {
    switchText.value = 'Switch language';
    isLangRus.value = false;
  } else {
    switchText.value = 'Сменить язык';
    isLangRus.value = true;
  }
};

provide('changeMonth', changeMonth);
</script>

<style lang="scss">
html {
  box-sizing: border-box;
}

body {
  margin: 0;
}

*,
::before,
::after {
  box-sizing: inherit;
}

.container {
  margin: 0 auto;
  max-width: 1110px;
  height: 98vh;

  .calendar {
    width: 50%;
    margin: 0 auto;
    padding: 10px;
    transform: translateY(10vh);
    border: 1px solid #000;
    border-radius: 5px;

    .calendar__header {
      display: flex;
      justify-content: space-between;
      padding: 10px 25px;
      border-bottom: 1px solid #000;

      .calendar__date {
        font-size: 20px;
      }
    }

    .calendar__names-day {
      display: flex;

      .list__item-name {
        padding: 10px;
        width: calc(100% / 7);
        text-align: center;
      }
    }

    .calendar__days {
      display: flex;
      flex-wrap: wrap;

      .list__item-day {
        padding: 10px;
        width: calc(100% / 7);
        color: #bcbcbc;
        text-align: center;
        cursor: pointer;
      }
    }
  }
}

.btn-reset {
  padding: 0;
  border: none;
  background-color: transparent;
  cursor: pointer;
}

.btn-switch {
  display: block;
  margin: 0 auto;
  padding: 10px;
  border: 1px solid #1061d1;
  color: #1061d1;
  transform: translateY(40%);
  transition: background-color .3s ease-in-out, color .3s ease-in-out;
}

.btn-switch:hover{
  background-color: #1061d1;
  color: #fff;
}

.list-reset {
  margin: 0;
  padding: 0;
  list-style-type: none;
}
</style>
