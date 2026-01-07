<script setup>
import { ref } from 'vue';
import Button from './components/Button.vue';
import Card from './components/Card.vue';
import Score from './components/Score.vue';

const scores = ref(0)
const cards = ref([
  {
    word: 'test',
    translation: 'тест',
    status: 'pending',
    state: 'closed',
  },
  {
    word: 'food',
    translation: 'еда',
    status: 'pending',
    state: 'closed',
  },
  {
    word: 'game',
    translation: 'игра',
    status: 'pending',
    state: 'closed',
  }
])

function turn(newState, number) {
  cards.value[number].state = newState
}

function changeStatus(newStatus, number) {
  cards.value[number].state = 'closed'
  cards.value[number].status = newStatus
  if (newStatus === 'success') {
    scores.value += 1
  }
}
</script>

<template>
  <main class="main">
    <header class="header">
      <div class="header-title">
        ЗАПОМНИ СЛОВО
      </div>
      <div>
        <Score :count="scores" />
      </div>
    </header>
    <div class="card-container">
      <div v-for="(value, ind) in cards" :key="ind" class="card-wrap">
        <Card 
            :status="value.status" :word="value.word" 
            :translation="value.translation" :number="ind"
            :state="value.state" 
            @turn="turn" 
            @change-status="changeStatus" 
          />
      </div>
    </div>
    <div class="button-line">
      <Button>Начать игру</Button>
    </div>
  </main>
</template>

<style scoped>
.main {
  background-color: var(--color-bg-main);
  border-radius: 25px;
  padding: 20px;
}

.card-container {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
  padding: 20px 0;
}

.card-wrap {
  width: calc(100% / 3 - 20px);
}

.header {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  align-items: center;
}

.button-line {
  text-align: center;
  padding: 20px 0;
}

.header-title {
  text-transform: capitalize;
  font-weight: 700;
  font-size: 16px;
  line-height: 24px;
}
</style>