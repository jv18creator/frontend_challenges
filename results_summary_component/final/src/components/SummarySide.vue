<script setup lang="ts">
import StatItem from '@/components/StatItem.vue'
const stateItems = [
  { name: 'Reaction', points: 80, className: 'reaction-txt' },
  { name: 'Memory', points: 92, className: 'memory-txt' },
  { name: 'Verbal', points: 61, className: 'verbal-txt' },
  { name: 'Visual', points: 80, className: 'visual-txt' }
]
</script>

<template>
  <div class="wrapper half-containers">
    <p class="summary-txt">Summary</p>
    <ul class="list-wrapper">
      <li v-for="(value, key) in stateItems" :key="key" :class="value.className" >
        <StatItem :stat="value" />
      </li>
    </ul>
    <button class="btn">Contiune</button>
  </div>
</template>

<style scoped>
  .btn {
    background: var(--btn-pm-clr);
    padding: 1.2rem 1rem;
    color: var(--text-white);
    font-size: 100%;
    border-radius: 40px;
    font-weight: 600;
    transition: all .3s ease;
    cursor: pointer;
  }

  .list-wrapper {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  .wrapper {
    gap: 3rem;
  }

  .list-wrapper li {
    padding: 12px 16px;
    border-radius: 12px;
    cursor: pointer;
    transition: all .3s ease;
  }

  .btn:hover {
    background: linear-gradient(hsla(256, 72%, 46%, .8), var(--color-violet));
  }

  .summary-txt {
    font-size: 140%;
    font-weight: 700;
  }
</style>
