<template>
  <div>
    <NuxtRouteAnnouncer />
    <NuxtPage />
  </div>
</template>

<script setup>
onMounted(() => {
  if (!localStorage.getItem("level")) {
    localStorage.setItem("level", "Mot")
  }
})
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Playwrite+DE+Grund:wght@100..400&display=swap');

* {
  font-family: "Playwrite DE Grund", cursive;
  font-optical-sizing: auto;
  font-style: normal;
}
</style>
