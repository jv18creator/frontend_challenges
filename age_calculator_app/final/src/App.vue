<script setup>
import DivideIcon from './assets/images/icon-arrow.svg'
import { ref, onUpdated, watch } from 'vue'

const day = ref(null)
const month = ref(null)
const year = ref(null)
const remainingDays = ref(null)
const remainingMonths = ref(null)
const remainingYears = ref(null)
const isDateValid = ref(null)

// Watch for changes in day, month, and year
watch(
  [day, month, year],
  ([newDay, newMonth, newYear], [oldDay, oldMonth, oldYear]) => {
    isDateValid.value = isValidDate(
      parseInt(newYear),
      parseInt(newMonth),
      parseInt(newDay)
    )
  }
)

function isValidDate(year, month, day) {
  const date = new Date(year, month - 1, day)
  const isValid =
    !isNaN(date) &&
    date.getFullYear() === year &&
    date.getMonth() === month - 1 &&
    date.getDate() === day
  return isValid
}

// Define the handleChange function
const handleChange = (e) => {
  const { name, value } = e.target
  if (name === 'year' && String(value).length < 5) {
    year.value = e.target.value
  } else if (String(value).length < 3 && name !== 'year') {
    // Use the variable's value property to update the reactive variable
    if (name === 'day') day.value = e.target.value
    else if (name === 'month') month.value = e.target.value
  }
}

onUpdated(() => {
  if (isDateValid.value) {
    const date = new Date(`${year.value}-${month.value}-${day.value}`)
    const { years, months, days } = calculateRemainingTime(date)
    remainingDays.value = days
    remainingMonths.value = months
    remainingYears.value = years
  } else {
    remainingDays.value = null
    remainingMonths.value = null
    remainingYears.value = null
  }
})

function calculateRemainingTime(givenDate) {
  const currentDate = new Date()
  const givenDateTime = givenDate.getTime()
  const currentDateTime = currentDate.getTime()
  const timeDiff = currentDateTime - givenDateTime

  // Convert time difference to years, months, and days
  const oneYearInMillis = 31536000000 // 1 year = 365 days * 24 hours * 60 minutes * 60 seconds * 1000 milliseconds
  const oneMonthInMillis = 2592000000 // 1 month = 30 days * 24 hours * 60 minutes * 60 seconds * 1000 milliseconds
  const oneDayInMillis = 86400000 // 1 day = 24 hours * 60 minutes * 60 seconds * 1000 milliseconds

  const remainingYears = Math.floor(timeDiff / oneYearInMillis)
  const remainingMonths = Math.floor(
    (timeDiff % oneYearInMillis) / oneMonthInMillis
  )
  const remainingDays = Math.floor(
    (timeDiff % oneMonthInMillis) / oneDayInMillis
  )

  return {
    years: remainingYears,
    months: remainingMonths,
    days: remainingDays,
  }
}
</script>

<template>
  <main class="app_wrapper">
    <header class="date_wrapper">
      <div>
        <label class="label" for="day">DAY</label>
        <input
          pattern="\d*"
          maxlength="2"
          name="day"
          type="text"
          :value="day"
          @input="handleChange"
        />
      </div>
      <div>
        <label class="label" for="month">MONTH</label>
        <input
          @input="handleChange"
          :value="month"
          pattern="\d*"
          maxlength="2"
          name="month"
          type="text"
        />
      </div>
      <div>
        <label class="label" for="year">YEAR</label>
        <input
          @input="handleChange"
          :value="year"
          type="text"
          name="year"
          id="year"
          required
          pattern="\d*"
          maxlength="4"
        />
      </div>
    </header>
    <div class="divide">
      <hr />
      <div>
        <DivideIcon class="img" />
      </div>
    </div>
    <div class="calculation_wrapper">
      <p>
        <span>{{ remainingYears || '- -' }}</span
        >years
      </p>
      <p>
        <span>{{ remainingMonths || '- -' }}</span
        >months
      </p>
      <p>
        <span>{{ remainingDays || '- -' }}</span
        >days
      </p>
    </div>
  </main>
</template>

<style scoped>
.app_wrapper {
  max-width: 920px;
  margin: 0 auto;
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 5rem;
  padding: 2rem;
  background-color: #fff;
  border-radius: 2rem 2rem 60% 2rem;
}

.date_wrapper {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  width: 100%;
  justify-content: start;
  gap: 2rem;
}

.date_wrapper div {
  width: 20%;
}

.label {
  font-weight: 500;
  letter-spacing: 4px;
  color: var(--smoke-grey);
}

input {
  width: 100%;
  font-size: 32px;
  font-weight: 700;
  padding: 1rem;
  outline: none;
  border-radius: 4px;
  border: 1px solid var(--border-clr);
  margin-top: 1rem;
}

input:focus {
  outline: 1px solid var(--pm-purpul);
  caret-color: var(--pm-purpul);
}

.calculation_wrapper {
  display: flex;
  justify-content: start;
  align-items: start;
  flex-direction: column;
  gap: 1rem;
}

.calculation_wrapper p,
span {
  font-weight: 700;
  font-size: 82px;
  margin-right: 4px;
  font-style: italic;
}

.calculation_wrapper span {
  color: var(--pm-purpul);
}

.divide {
  height: 1px;
  position: relative;
}

.divide div {
  padding: 20px;
  border-radius: 100%;
  background-color: var(--pm-purpul);
  position: absolute;
  top: 50%;
  transform: translate(0, -50%);
  right: 0%;
  transition: 0.3s ease;
}

.divide div:hover {
  background-color: var(--off-black);
}

hr {
  background-color: var(--border-clr);
  height: 1px;
  border: none;
}

@media only screen and (max-width: 620px) {
  .date_wrapper div {
    width: 100%;
  }

  .date_wrapper input {
    width: 100%;
    padding: 1rem;
    font-size: 22px;
  }

  .divide div {
    transform: translate(50%, -50%);
    right: 50%;
  }

  .app_wrapper {
    border-radius: 2rem 2rem 2rem 2rem;
  }

  .date_wrapper {
    gap: 0.5rem;
  }

  .label {
    font-size: 12px;
  }

  input {
    padding: 1rem .75rem !important;
    margin-top: .75rem;
  }
}

@media (max-width: 801px) {
  .calculation_wrapper {
    gap: 0;
  }

  .calculation_wrapper p,
  span {
    font-size: 60px;
  }
}
</style>
