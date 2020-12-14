<template>
  <div class="income-list">
    <IncomeItem
      v-for="obj in state.incomeFiltered"
      :key="obj.id"
      :income="obj"
      @removeItem="removeItem"
    />
  </div>
</template>

<script>
import IncomeItem from "./IncomeItem";
export default {
  props: {
    state: Object,
  },
  setup(props, { emit }) {
    function removeItem(id) {
      emit("removeItem", id);
    }

    return {
      IncomeItem,
      removeItem,
    };
  },
};
</script>

<style scoped>
.income-list {
  margin-top: 30px;
  padding: 15px;
  max-height: 40vh;
  overflow: scroll;
}
</style>
