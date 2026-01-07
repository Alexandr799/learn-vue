<script setup>
import Button from './components/Button.vue';
import Card from './components/Card.vue';
import Score from './components/Score.vue';


</script>

<template>
  <main class="main">
    <header class="header">
      <div class="header-title">
        ЗАПОМНИ СЛОВО
      </div>
      <div>
        <Score count="100" />
      </div>
    </header>
    <div style="padding: 20px;">
      <Card word="Test" translate="Тест" number="01"/>
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