<script setup lang="ts">
import SummarySide from '@/components/SummarySide.vue'
import ResultSide from '@/components/ResultSide.vue'
</script>

<template>
  <main>
    <ResultSide />
    <SummarySide />
  </main>
</template>

<style scoped>
main {
  display: flex;
  width: 100%;
  justify-content: center;
  border-radius: 2rem;
}

@media only screen and (max-width: 600px) {
  main {
    border-radius: 0;
    flex-direction: column;
  }
}
</style>
