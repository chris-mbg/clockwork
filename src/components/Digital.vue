<template>
  <div class="digital">
    <span class="hms">{{ time }}</span>
    <span class="date">{{ date }}</span>
  </div>
</template>

<script lang="ts" setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';

const time = ref("")
const date = ref("")

const updateTime = () => {
  const dateInfo = new Date()

  time.value = dateInfo.toLocaleTimeString('sv-SE', { hour: "numeric", minute: "numeric"})
  date.value = dateInfo.toLocaleDateString('sv-SE', {  weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })
}

let stop: number;
onMounted(() => {
  stop = setInterval(() => updateTime(), 1000)
})

onBeforeUnmount(() => clearInterval(stop))

</script>

<style lang="scss" scoped>
.digital {
  font-family: 'Rajdhani', sans-serif;
    background:#0f1115;
    text-align: center;
    width: 380px;
    border: 6px solid #cacaca;
    padding: 8px;
    box-shadow: 0 2px 10px 0 rgba(0,0,0,0.16), 0 2px 10px 0
    rgba(0,0,0,0.12);
    border-radius: 20%;
    margin: 20px auto;

    display:grid;
    grid-template-rows: auto auto;
}
.hms {
    font-size: 68pt;
    font-weight: 500;
}
.date {
    font-size: 15pt;
    font-weight: 300;
}

</style>