<script setup lang="ts"></script>

<template>
  <div class="wrapper half-containers result-wrapper">
    <p class="result-txt">Your Result</p>
    <div class="progress-wrapper">
      <h4>76</h4>
      <p>of 100</p>
    </div>
    <p class="great-txt">Great</p>
    <p>You scored higher than 65% of the people who have taken these tests.</p>
  </div>
</template>

<style scoped>
.progress-wrapper {
  display: flex;
  flex-direction: column;
  padding: 1.6rem 3rem;
  border-radius: 100%;
  box-shadow: inset 0px 10px 20px 2px rgba(0, 0, 0, 0.25);
}

.progress-wrapper h4 {
  font-size: 4rem;
  line-height: normal;
  font-weight: 700;
}

.progress-wrapper p {
  color: var(--color-light-lavender);
  font-weight: 600;
}

.result-wrapper {
  background: linear-gradient(hsla(234, 85%, 45%, 0.6) -10%, hsl(234, 85%, 45%, 1));
  color: var(--text-white);
  border-radius: 2rem;
  align-items: center;
  text-align: center;
}

.result-txt {
  font-weight: 700;
  color: var(--color-light-lavender);
  font-size: 125%;
}

.great-txt {
  font-size: 150%;
  font-weight: 700;
}

@media only screen and (max-width: 600px) {
  .result-wrapper {
    border-radius: 0 0 2rem 2rem;
  }
}
</style>
