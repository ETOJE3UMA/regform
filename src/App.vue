<template>
  <form @submit.prevent="someAction()">
    <div class="field">
      <label for="name">Имя</label>
      <input
        v-model="name"
        type="name"
        @blur="isNameTouched = true"
        :class="{ error: isNameError }"
      >
      <div v-if="isNameError">Введено не корректное значение</div>
    </div>
    <div class="field">
      <label for="email">Email</label>
      <input
        v-model="email"
        type="email"
        @blur="isEmailTouched = true"
        :class="{ error: isEmailError }"
      >
      <div v-if="isEmailError">Введено не корректное значение</div>
    </div>
    <div class="field">
      <label for="tel">Телефон</label>
      <input
        v-model="tel"
        type="tel"
        @blur="isTelTouched = true"
        :class="{ error: isTelError }"
      >
      <div v-if="isTelError">Введено не корректное значение</div>
    </div>

    <button type="submit" :disabled="!isFormValid">
      Отправить форму
    </button>
  </form>
</template>

<script>
//eslint-disable-next-line
const emailCheckRegex = /^(([^<>()\[\]\.,;:\s@\"]+(\.[^<>()\[\]\.,;:\s@\"]+)*)|(\".+\"))@(([^<>()[\]\.,;:\s@\"]+\.)+[^<>()[\]\.,;:\s@\"]{2,})$/i;
//eslint-disable-next-line
const nameCheckRegex = /^[a-zа-я]+(-[a-zа-я]+( [a-zа-я]+)?||( [a-zа-я]+)(-[a-zа-я]+)?)?$/i;
//eslint-disable-next-line
const telCheckRegex = /^\+?[78][-\(]?\d{3}\)?-?\d{3}-?\d{2}-?\d{2}$/;

export default {
  data() {
    return {
      email: null,
      isEmailTouched: false,
      name: null,
      isNameTouched: false,
      tel: null,
      isTelTouched: false
    };
  },

  computed: {
    //Проверка электронной почты
    isEmailValid() {
      return emailCheckRegex.test(this.email);
    },
    isEmailError() {
      return !this.isEmailValid && this.isEmailTouched;
    },
    //Проверка имени
    isNameValid() {
      return nameCheckRegex.test(this.name);
    },
    isNameError() {
      return !this.isNameValid && this.isNameTouched;
    },
    //Проверка телефона
    isTelValid() {
      return telCheckRegex.test(this.tel);
    },
    isTelError() {
      return !this.isTelValid && this.isTelTouched;
    },
    //Форма заполнена правильно
    isFormValid() {
      return this.isEmailValid && this.isNameValid && this.isTelValid;
    }
  },
  methods: {
    someAction() {
      if (!this.isEmailValid && !this.isNameValid && !this.isTelValid) {
        return;
      }
      alert("Форма отправлена");
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
