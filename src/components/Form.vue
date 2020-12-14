<template>
  <form class="form" @submit.prevent="formHandler" @change="validateForm">
    <select class="form__select" v-model="formData.category" required>
      <option>Зарплата</option>
      <option>Одежда</option>
      <option>Еда</option>
      <option>Транспорт</option>
      <option>Дом и связь</option>
      <option>Развлечения</option>
      <option>Лекарства</option>
    </select>
    <input
      required
      class="form__input form__input_description"
      type="text"
      placeholder="Добавьте описание"
      v-model="formData.desc"
    />
    <input
      required
      class="form__input form__input_number"
      type="number"
      placeholder="Добавьте сумму"
      v-model="formData.value"
    />
    <select required class="form__select" v-model="formData.type">
      <option selected>Доходы</option>
      <option>Расходы</option>
    </select>
    <button disabled class="form__button form__button_disabled" type="submit">
      +
    </button>
  </form>
</template>

<script>
import { reactive } from "vue";

export default {
  props: {
    state: Object,
  },
  setup(props, { emit }) {
    const formData = reactive({
      desc: null,
      value: null,
      type: null,
      category: null,
    });

    function formHandler() {
      emit("addIncome", {
        desc: formData.desc,
        value: formData.value,
        type: formData.type,
        category: formData.category,
      });

      formData.desc = null;
      formData.value = null;
      formData.type = null;
      formData.category = null;
    }

    function validateForm(event) {
      const button = event.target.parentElement.querySelector(".form__button");
      if (event.target.parentElement.checkValidity()) {
        button.disabled = false;
        button.classList.add("form__button_active");
        button.classList.remove("form__button_disabled");
      } else {
        button.disabled = true;
        button.classList.remove("form__button_active");
        button.classList.add("form__button_disabled");
      }
    }

    return {
      formHandler,
      formData,
      validateForm,
    };
  },
};
</script>

<style scoped>
.form {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

.form__select {
  border: 1px solid #121212;
  margin-right: 10px;
}

.form__select:focus {
  outline: none;
}

.form__input {
  color: #121212;
  border: none;
  outline: none;
  font-size: 16px;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.form__input::placeholder {
  color: #aaa;
  font-size: 16px;
}

.form__input_description,
.form__input_number {
  margin-right: 10px;
}

.form__button {
  display: block;
  background: none;
  border: none;
  outline: none;
  color: #fff;
  font-weight: 500;
  font-size: 28px;
  padding: 5px 15px;
  transition: 0.2s ease-in-out;
}

.form__button_disabled {
  background-color: #aaa;
  cursor: not-allowed;
}

.form__button_disabled:hover {
  background-color: #ccc;
}

.form__button_active {
  background-color: #ffce00;
  cursor: pointer;
}

.form__button_active:hover {
  background-color: #00aeff;
}

@media screen and (max-width: 1024px) {
  .form__button {
    font-size: 18px;
  }
}

@media screen and (max-width: 1024px) {
  .form__input,
  .form__input::placeholder {
    font-size: 14px;
  }
}

@media screen and (max-width: 800px) {
  .form {
    flex-direction: column;
    width: 50%;
    margin: 0 auto;
  }

  .form__select {
    margin-bottom: 5px;
    padding: 10px;
    margin-right: 0;
  }

  .form__input {
    margin-bottom: 5px;
    margin-right: 0;
  }

  .form__button {
    margin-bottom: 5px;
  }
}

@media screen and (max-width: 500px) {
  .form {
    width: 90%;
  }
}
</style>
