<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style lang="scss" scoped>
header {
  width: 100%;
  background-color: #222222;
  padding: 2rem;
  box-shadow: 0 -3px 10px 1px orange;
  text-align: center;

  a {
    color: orange;
    text-decoration: none;
    text-transform: uppercase;
    font-size: 1.5 rem;
  }
}
</style>
