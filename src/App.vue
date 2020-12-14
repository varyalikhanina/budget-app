<template>
  <div class="container">
    <Header
      :totalIncome="state.totalIncome"
      :incomes="state.onlyIncomesFormat"
      :expenses="state.onlyExpensesFormat"
      :percentage="state.expensesPercentage"
    />
    <div class="wrapper">
      <Form :state="state" @addIncome="addIncome" />
      <Sort @change="changeFilterWord" />
    </div>
    <IncomeList :state="state" @removeItem="removeItem" />
  </div>
</template>

<script>
import { reactive, computed, onMounted } from "vue";
import numeral from "numeral";
import Header from "./components/Header";
import Form from "./components/Form";
import IncomeList from "./components/IncomeList";
import Sort from "./components/Sort";

export default {
  setup() {
    onMounted(() => {
      if (localStorage.income) {
        const parsedItems = JSON.parse(localStorage.income);
        parsedItems.forEach((item) => {
          state.incomeFiltered.push(item);
          state.income.push(item);
        });
      }
    });
    const state = reactive({
      income: [],
      incomeFiltered: [],
      filter: "Все",
      totalIncome: computed(() => {
        let temp = 0;
        if (state.income.length > 0) {
          for (let i = 0; i < state.income.length; i++) {
            if (state.income[i].type == "Доходы") {
              temp += state.income[i].value;
            } else {
              temp -= state.income[i].value;
            }
          }
          return numeral(temp).format("0,0.00");
        } else {
          return 0;
        }
      }),
      onlyIncomes: computed(() => {
        let onlyIncomes = 0;
        state.income.forEach((el) => {
          if (el.type == "Доходы") {
            onlyIncomes += el.value;
          } else {
            return 0;
          }
        });
        return onlyIncomes;
      }),
      onlyIncomesFormat: computed(() => {
        return numeral(state.onlyIncomes).format("0,0.00");
      }),
      onlyExpenses: computed(() => {
        let onlyExpenses = 0;
        state.income.forEach((el) => {
          if (el.type == "Расходы") {
            onlyExpenses += el.value;
          } else {
            return 0;
          }
        });
        return onlyExpenses;
      }),
      onlyExpensesFormat: computed(() => {
        return numeral(state.onlyExpenses).format("0,0.00");
      }),
      expensesPercentage: computed(() => {
        if (
          (state.onlyExpenses == 0 && state.onlyIncomes == 0) ||
          state.onlyExpenses == 0
        ) {
          return "0%";
        } else if (state.onlyExpenses !== 0 && state.onlyIncomes == 0) {
          return `Введите данные о доходах. Расходы превышают доход на ${state.onlyExpenses}₽`;
        } else {
          return (
            ((state.onlyExpenses * 100) / state.onlyIncomes).toFixed(2) + "%"
          );
        }
      }),
    });

    function changeFilterWord(event) {
      state.filter = event.target.value;
      if (event.target.value === "Все") {
        state.incomeFiltered = state.income;
      } else if (event.target.value !== "Все") {
        state.incomeFiltered = state.income.filter(
          (v) => v.category === state.filter
        );
      }
    }

    function addIncome(obj) {
      state.income = [
        ...state.income,
        {
          id: Date.now(),
          desc: obj.desc,
          type: obj.type,
          category: obj.category,
          value: parseInt(obj.value),
        },
      ];
      state.incomeFiltered = state.income;
      const itemsToAdd = state.income;
      localStorage.setItem("income", JSON.stringify(itemsToAdd));
    }

    function removeItem(id) {
      state.income = state.income.filter((v) => v.id != id);
      state.incomeFiltered = state.incomeFiltered.filter((v) => v.id != id);
      const itemDeleted = state.income;
      localStorage.setItem("income", JSON.stringify(itemDeleted));
    }

    return {
      Header,
      IncomeList,
      Form,
      Sort,
      state,
      addIncome,
      removeItem,
      changeFilterWord,
    };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}
#app {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.container {
  width: 90%;
}
.wrapper {
  display: flex;
  justify-content: center;
}

@media screen and (max-width: 800px) {
  .wrapper {
    flex-direction: column;
  }
}
</style>
