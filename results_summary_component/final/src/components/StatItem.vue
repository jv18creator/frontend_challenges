<script setup lang="ts">
defineProps({
  stat: {
    type: Object as () => { name: string, points: number, className: string },
    required: true
  }
})
</script>

<template>
  <div class="stat-wrapper">
    <p class="txt">{{ stat.name }}</p>
    <p class="points"><span>{{ stat.points }}</span> / 100</p>
  </div>
</template>

<style scoped>
.stat-wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

span {
  color: var(--btn-pm-clr);
  font-weight: 700;
}

.points {
  color: #000;
}

p {
  font-size: 120%;
}

</style>