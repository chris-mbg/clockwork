<template>
  <div class="clock">
    <div class="clock-face" ref="clockFace">
      <time datetime="12:00">12</time>
      <time datetime="1:00">1</time>
      <time datetime="2:00">2</time>
      <time datetime="3:00">3</time>
      <time datetime="4:00">4</time>
      <time datetime="5:00">5</time>
      <time datetime="6:00">6</time>
      <time datetime="7:00">7</time>
      <time datetime="8:00">8</time>
      <time datetime="9:00">9</time>
      <time datetime="10:00">10</time>
      <time datetime="11:00">11</time>

      <span class="arm seconds"></span>
      <span class="arm minutes"></span>
      <span class="arm hours"></span>
      <span class="arm center"></span>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, watch } from "vue"

const clockFace = ref()

const time = new Date()
const hour = -3600 * (time.getHours() % 12)
const mins = -60 * time.getMinutes()

watch(clockFace, () => {
  if(clockFace.value) {
    clockFace.value.style.setProperty("--delayHours", `${hour + mins}s`)
    clockFace.value.style.setProperty("--delayMin", `${mins}s`)
  }
})



</script>

<style lang="scss" scoped>

// $outerWidth: clamp(5rem, 60vw, 40rem);
$outerWidth: 400px;
$width: 360px;
$numSize: 36px;
$radius: calc( ($width - $numSize) / 2);
@debug "radius #{$radius}";

@function getX($degree) {
  @return calc($radius + $radius * cos($degree));
}

@function getY($degree) {
  @return calc($radius + $radius * sin($degree));
}

@mixin position($degree) {
  left: getX($degree);
  top: getY($degree);
}

.clock {
  margin: 40px auto;
  background-color: #0f1115;
  border-radius: 24%;
  // box-shadow: 1px 1px 10px 1px orange;
  container-type: inline-size;
  display: grid;
  place-content: center;
  height: $outerWidth;
  width: $outerWidth;

  .clock-face {
    position: relative;
    width: $width;
    height: $width;
    border-radius: 50%;
    background-color: #eee;
    aspect-ratio: 1;

    time {
      display: grid;
      place-content: center;
      position: absolute;
      height: $numSize;
      width: $numSize;
      font-weight: 900;
      font-size: 20px;
      color: #0f1115;
    }

    time:nth-child(1) {
      @include position($degree: 270deg)
    }
    time:nth-child(2) {
      @include position($degree: 300deg)
    }
    time:nth-child(3) {
      @include position($degree: 330deg)
    }
    time:nth-child(4) {
      @include position($degree: 0deg)
    }
    time:nth-child(5) {
      @include position($degree: 30deg)
    }
    time:nth-child(6) {
      @include position($degree: 60deg)
    }
    time:nth-child(7) {
      @include position($degree: 90deg)
    }
    time:nth-child(8) {
      @include position($degree: 120deg)
    }
    time:nth-child(9) {
      @include position($degree: 150deg)
    }
    time:nth-child(10) {
      @include position($degree: 180deg)
    }
    time:nth-child(11) {
      @include position($degree: 210deg)
    }
    time:nth-child(12) {
      @include position($degree: 240deg)
    }

    @mixin arm($bg, $armW, $armH) {
      background-color: $bg;
      border-radius: calc($armW * 2);
      display: block;
      height: $armH;
      left: calc(($width - $armW) / 2);
      position: absolute;
      top: calc(($width / 2) - $armH);
      transform: rotate(0deg);
      transform-origin: bottom;
      width: $armW;
    }

    @keyframes turn {
      to {
        transform: rotate(1turn)
      }
    }

    .arm.hours {
      @include arm($bg: #111, $armW: 10px, $armH: 120px);
      animation: turn 43200s linear infinite;
      animation-delay: var(--delayHours, 0ms);


      &::before {
        background-color: #eee;
        border: 1cqi solid #333;
        border-radius: 50%;
        content: "";
        display: block;
        height: 4cqi;
        position: absolute;
        bottom: -3cqi;
        left: -1.75cqi;
        width: 4cqi;
      }
    }
    .arm.minutes {
      @include arm($bg: #111, $armW: 10px, $armH: 145px);
      animation: turn 3600s steps(60, end) infinite;
      animation-delay: var(--delayMin, 0ms);
    }
    .arm.seconds {
      @include arm($bg: orange, $armW: 5px, $armH: 150px);
      animation: turn 60s steps(60, end) infinite;
    }
  }
}
</style>
