<template>
  <header class="header">
    <h1 class="header__title">Доступный бюджет</h1>
    <p class="header__budget">{{ totalIncome }} ₽</p>
    <p class="header__income">Доходы + {{ incomes }} ₽</p>
    <p class="header__expense">Расходы - {{ expenses }} ₽ ({{ percentage }})</p>
  </header>
</template>

<script>
export default {
  props: ["totalIncome", "incomes", "expenses", "percentage"],
};
</script>

<style scoped>
.header {
  padding: 15px 30px;
  text-align: center;
}

.header__title {
  font-size: 28px;
  margin: 20px;
  color: #121212;
}

.header__budget {
  color: #fff;
  font-size: 24px;
  color: #121212;
}

.header__income,
.header__expense {
  font-size: 16px;
  margin: 5px;
}

@media screen and (max-width: 800px) {
  .header__title {
    font-size: 24px;
    margin: 10px;
  }
  .header__budget {
    font-size: 20px;
  }
  .header__income,
  .header__expense {
    font-size: 14px;
  }
}
@media screen and (max-width: 500px) {
  .header {
    padding: 5px;
  }
}
</style>
