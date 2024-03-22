<template>
  <div class="calendar">
    <div class="calendar__header">
      <button class="calendar__btn-pre btn-reset">
        <ArrowDicrementSVG/>
      </button>
      <span class="calendar__date">text</span>
      <button class="calendar__btn-next btn-reset">
        <ArrowIncrementSVG/>
      </button>
    </div>
    <ul class="list calendar__names-day list-reset">
      <li class="list__item-name">
        weekday
      </li>
    </ul>
    <ul class="list calendar__days list-reset">
      <li class="list__item-day" v-for="day in 31" :key="day">
        {{ day }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import ArrowDicrementSVG from './componentsSVG/ArrowDicrementSVG.vue';
import ArrowIncrementSVG from './componentsSVG/ArrowIncrementSVG.vue';
</script>
