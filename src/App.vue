<script setup>
import { onMounted, ref } from 'vue';
import Button from './components/Button.vue';
import Card from './components/Card.vue';
import Score from './components/Score.vue';

const API = 'http://localhost:8080/api/random-words'
const scores = ref(0)
const cards = ref([])
const error = ref(null)
const loading = ref(false)
const firstGame = ref(true)
const update = async () => {
  firstGame.value = false
  scores.value = 0
  try {
    loading.value = true
    let res = await fetch(API);
    if (res.status !== 200) {
      error.value = 'Что-то пошло не так!'
      return
    }
    res = await res.json()
    error.value = null
    cards.value = res.map(el => ({
      word: el.word,
      translation: el.translation,
      status: 'pending',
      state: 'closed',
    }))
  } catch {
    error.value = 'Что-то пошло не так!'
    return
  } finally {
    loading.value = false
  }
}

function turn(newState, number) {
  cards.value[number].state = newState
}

function changeStatus(newStatus, number) {
  cards.value[number].state = 'closed'
  cards.value[number].status = newStatus
  if (newStatus === 'success') {
    scores.value += 10
  }

  if (newStatus === 'fail') {
    scores.value -= 4
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
    <div class="card-container" v-if="!loading">
      <template v-if="!error">
        <div v-for="(value, ind) in cards" :key="ind" class="card-wrap">
          <Card :status="value.status" :word="value.word" :translation="value.translation" :number="ind"
            :state="value.state" @turn="turn" @change-status="changeStatus" />
        </div>
      </template>
      <div v-else>
        {{ error }}
      </div>
    </div>
    <div v-else class="card-container">
      Загрузка
    </div>
    <div class="button-line">
      <Button @click="update">{{ firstGame ? 'Начать игру' : 'Начать заново' }}</Button>
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