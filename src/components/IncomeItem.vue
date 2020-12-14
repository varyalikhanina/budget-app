<template>
  <div class="income-item">
    <img
      @click="removeItem"
      class="income-remove"
      alt="Удалить запись"
      src="https://icons-for-free.com/iconfiles/png/512/delete+remove+trash+trash+bin+trash+can+icon-1320073117929397588.png"
    />
    <p class="income-description">
      {{ income.desc }}
    </p>
    <p class="income-price">{{ income.value }} ₽</p>
    <p class="income-type">{{ income.category }}</p>
    <p class="income-type">{{ income.type }}</p>
  </div>
</template>

<script>
export default {
  props: {
    income: Object,
  },
  setup(props, { emit }) {
    function removeItem() {
      emit("removeItem", props.income.id);
    }

    return {
      removeItem,
    };
  },
};
</script>

<style scoped>
.income-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px 15px 15px 0px;
  background-color: #fff;
  width: 500px;
  margin: 0 auto 10px;
}

.income-remove {
  width: 30px;
  height: 30px;
  margin-right: 10px;
  cursor: pointer;
}

.income-description,
.income-price,
.income-type {
  color: #666;
  min-width: 100px;
  font-size: 16px;
}

@media screen and (max-width: 800px) {
  .income-item {
    width: 90%;
  }

  .income-description,
  .income-price,
  .income-type {
    font-size: 12px;
    min-width: 50px;
  }
}

@media screen and (max-width: 500px) {
  .income-item {
    padding: 0;
    width: 100%;
  }
  .income-description,
  .income-price,
  .income-type {
    font-size: 10px;
  }
}
</style>
