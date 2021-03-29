<template>
  <form @submit.prevent="someAction()">
    <div class="header-form">
      <h1>
        Регистрация
      </h1>
      <p>
        Уже есть аккаунт? <a href="#">Войти</a>
      </p>
    </div>
    <div class="field">
      <label for="name">Имя</label>
      <input
        v-model="name"
        type="name"
        placeholder="Введите Ваше имя"
        @blur="isNameTouched = true"
        :class="{ error: isNameError }"
      >
      <div class="error" v-if="isNameError">Введено не корректное значение</div>
    </div>
    <div class="field">
      <label for="email">Email</label>
      <input
        v-model="email"
        type="email"
        placeholder="Введите ваш email"
        @blur="isEmailTouched = true"
        :class="{ error: isEmailError }"
      >
      <div class="error" v-if="isEmailError">Введено не корректное значение</div>
    </div>
    <div class="field">
      <label for="tel">Номер телефона</label>
      <input
        v-model="tel"
        type="tel"
        placeholder="Введите ваш номер телефона"
        @blur="isTelTouched = true"
        :class="{ error: isTelError }"
      >
      <div class="error" v-if="isTelError">Введено не корректное значение</div>
    </div>
    <div class="field check">
      <input type="checkbox" class="checkbox" id="checkbox1" />
      <label for="checkbox1">Принимаю <a href="#">условия</a> пользования</label>
    </div>
    <button type="submit" :disabled="!isFormValid">
      Зарегистрироваться
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
/* Глобальные стили */
body {
  background-color: #E5E5E5;
  font-family: IBM Plex Sans;
  color: #2C2738;
}
a {
  color: #0880AE;
  text-decoration: none;
}
/* Стили формы */
form {
  position: absolute;
  left: 50%;
  transform: translate(-50%);
  background-color: #fff;
  width: 460px;
  height: auto;
  border-radius: 24px;
  box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.02), 0px 32px 64px rgba(44, 39, 56, 0.04);
  padding: 0 30px;
}
label {
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 21px;
  color: #756F86;
}
input {
  width: 100%;
  height: 52px;
  margin-top: 6px;
  margin-bottom: 8px;
  border: 1px solid #DBE2EA;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
  border-radius: 6px;
  font-size: 16px;
  line-height: 21px;
  color: #2C2738;;
  padding-left: 16px;
}
.header-form {
  margin-top: 40px;
  margin-bottom: 56px;
}
.field {
  margin-bottom: 8px;
}
.check {
  display: flex;
  align-items: center;
  margin-top: 35px;
}
/* Стили ошибки */
.error {
  font-family: IBM Plex Sans;
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 18px;
  color: #FF7171;
}
/* Стили кнопки в форме */
button {
  width: 100%;
  padding: 18px 121px;
  margin: 40px 0;
  border-radius: 6px;
  border: none;
  background: #0880AE;
  box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08), 0px 4px 8px rgba(44, 39, 56, 0.08);
  color: #EBF4F8;
  cursor: pointer;
}
button:disabled {
  background: #DBE2EA;
  color: #B1B5BF;
}
/* Стили чекбокса в форме */
.checkbox {
    position: absolute;
    z-index: -1;
    opacity: 0;
}
.checkbox + label {
    position: relative;
    vertical-align: middle;
    padding: 0 0 0 36px;
    cursor: pointer;
}
/* Чекбокс в состоянии неактивен */
.checkbox + label:before {
    content: '';
    position: absolute;
    top: -1px;
    left: 0;
    width: 26px;
    height: 26px;
    background: #FFFFFF;
    border: 1px solid #DBE2EA;
    box-sizing: border-box;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    border-radius: 4px;
}
/* Чекбокс в состоянии активен */
.checkbox + label:after {
    content: '';
    position: absolute;
}
/* Фон чекбокса в состоянии активен */
.checkbox:checked + label:after {
    position: absolute;
    top: -1px;
    left: 0;
    background-image: url(./assets/Icon.png);
    height: 26px;
    width: 26px;
    border: 1px solid #0880AE;
    box-sizing: border-box;
    box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
    border-radius: 4px;
}
/* Стили текстового инпута в форме */
input::placeholder {
  font-family: IBM Plex Sans;
  padding: 16px 0;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  color: #7C9CBF;
}
input:focus {
  border: 2px solid #0880AE;
  outline: none;
}

</style>
