<template>
  <select class="sort">
    <option selected>Все</option>
    <option>Зарплата</option>
    <option>Одежда</option>
    <option>Еда</option>
    <option>Транспорт</option>
    <option>Дом и связь</option>
    <option>Развлечения</option>
    <option>Лекарства</option>
  </select>
</template>

<script></script>

<style scoped>
.sort {
  position: relative;
  border: 1px solid #00aeff;
  outline: none;
  color: #00aeff;
  cursor: pointer;
  padding: 10px;
  font-weight: bold;
  margin-left: 10px;
  margin-top: 30px;
  font-size: 14px;
}

@media screen and (max-width: 1024px) {
  .sort {
    font-size: 12px;
  }
}

@media screen and (max-width: 800px) {
  .sort {
    width: 50%;
    margin: 0 auto;
  }
}

@media screen and (max-width: 500px) {
  .sort {
    width: 90%;
  }
}
</style>
