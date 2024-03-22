<template>
  <div class="calendar">
    <div class="calendar__header">
      <button class="calendar__btn-pre btn-reset"
      @click="changeMonth(-1)">
        <ArrowDicrementSVG/>
      </button>
      <span class="calendar__date">{{ headerDate }}</span>
      <button class="calendar__btn-next btn-reset"
      @click="changeMonth(+1)">
        <ArrowIncrementSVG/>
      </button>
    </div>
    <ul class="list calendar__names-day list-reset">
      <li class="list__item-name" v-for="weekday in weekdays" :key="weekday">
        {{ weekday }}
      </li>
    </ul>
    <ul class="list calendar__days list-reset">
      <li class="list__item-day" v-for="day in props.days" :key="day.id"
      :class="[{ 'list__item-day--current-month': day.currentMonth },
      { 'list__item-day--active': props.currentDay === day.date
      && isActive }]">
        {{ day.date }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { computed, defineProps, inject } from 'vue';
import ArrowDicrementSVG from './componentsSVG/ArrowDicrementSVG.vue';
import ArrowIncrementSVG from './componentsSVG/ArrowIncrementSVG.vue';

const months = [
  'January', 'February', 'March',
  'April', 'May', 'June',
  'July', 'August', 'September',
  'October', 'November', 'December'];
const weekdays = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

const props = defineProps({
  date: Object,
  currentDay: Number,
  currentMonth: Number,
  currentYear: Number,
  days: Object,
});

const headerDate = computed(() => {
  return props.date.toLocaleString('en-US', {
    month: 'long',
    year: 'numeric',
  });
});

const changeMonth = inject('changeMonth');

const isActive = computed(() => {
  return headerDate.value.split(' ').includes(months[props.currentMonth]) && headerDate.value.split(' ').includes(String(props.currentYear));
});
</script>
