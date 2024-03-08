<template>
  <div>
  <form v-if="isSent == false" @submit.prevent="submitForm" class="form-window">
    <h1>Регистрация</h1>
    <hr>
    <div>
      <span>Заполните Ваши данные</span>
      <div class="input">
        <div class="input__column">
          <div class="input-container">
            <input placeholder="Имя" type="text" v-model="formData.username" id="username">
            <span v-if="formErrors.username" class="error">{{ formErrors.username }}</span>
          </div>
          <div class="input-container">
            <div class="password">
            <input  placeholder="Пароль" :type=passwordType id="password" v-model="formData.password">
            <span v-if="formErrors.password" class="error">{{ formErrors.password }}</span>
            <button class="show" type="button" v-on:click="passwordVisibility" >
              <img v-if="showPassword == false" src="../assets/showed.svg" alt="">
              <img v-else src="../assets/hided.svg" alt="">
            </button>
          </div>
          </div>
          
        </div>
        <div class="input__column">
          <div class="input-container">
            <input placeholder="Email" type="email" id="email" v-model="formData.email" >
            <span v-if="formErrors.email" class="error">{{ formErrors.email }}</span>
          </div>
          <div class="input-container">
            <select id="role" required>
              <option value="" disabled selected hidden>Должность</option>
              <option v-for="option in roleOptions" :key="option.value" :value="option.value" >{{ option.name }}</option>
            </select>
          </div>
          <div class="input-container">
            <div class="password">
            <input placeholder="Повторите пароль" :type=passwordTypeRepeat id="password_repeat" v-model="formData.password_repeat" >
            <span v-if="formErrors.password_repeat" class="error">{{ formErrors.password_repeat }}</span>
            <span v-if="formErrors.passwords" class="error">{{ formErrors.passwords }}</span>
            <button class="show" type="button" v-on:click="passwordVisibilityRepeat" >
              <img v-if="showPasswordRepeat == false" src="../assets/showed.svg" alt="">
              <img v-else src="../assets/hided.svg" alt="">
            </button>
          </div>
          </div>
        </div>
      </div>
    </div>
    <hr>
    <div class="another">
      <div class="another__input">
        <div class="input-container">
          <label class="switch">
              <input type="checkbox" v-model="formData.public">
            <div class="slider round">
            </div>
          </label>
          <span id="public-error" v-if="formErrors.public" class="error">{{ formErrors.public }}</span>
        </div>
        <div>
          <span class="another__input__text">Хотите чтобы Ваш профиль видели другие участники платформы? </span>
          <span class="another__text">Включает профиль для просмотра другими пользователями по ссылке</span>
        </div>
      </div>
    </div>
    <div class="submit">
      <div class="submit__text">
        <div class="input-container">
          <input type="checkbox" v-model="formData.confidentiality" required>
          <span v-if="formErrors.confidentiality" class="error">{{ formErrors.confidentiality }}</span>
        </div>
        <span class="submit__text__input">Регистрируясь, Вы соглашаетесь  с <span class="blue-text">политикой конфиденциальности</span>  и обработкой <span class="blue-text">персональных данных</span> </span>
      </div>
      <button type="submit" class="submit__button">
        Зарегистрироваться
      </button>
    </div>
  </form>
  <div v-if="isSent == true" class="success">
    Регистрация успешно завершена!
  </div>
</div>
</template>

<script>
export default {
  name: "InputForm",
  data() {
    return {
      formData: {
        public: true,
        username: '',
        role: null,
        email: '',
        password: '',
        password_repeat: '',
        passwords: '',
        confidentiality: true
      },
      roleOptions: [
        { value: 1, name: 'Директор' },
        { value: 2, name: 'Менеджер' },
        { value: 3, name: 'Работник' }
      ],
      formErrors: {},
      registrationSuccess: false,
      showPassword: false,
      passwordType: "password",
      showPasswordRepeat: false,
      passwordTypeRepeat: "password",
      isSent: false
    };
  },
  methods: {
    passwordVisibility(){
      this.showPassword = this.showPassword == false ? true : false;
      this.passwordType = this.passwordType == 'password' ? 'text' : 'password';
    },
    passwordVisibilityRepeat(){
      this.showPasswordRepeat = this.showPasswordRepeat == false ? true : false;
      this.passwordTypeRepeat = this.passwordTypeRepeat == 'password' ? 'text' : 'password';
    },
    submitForm() {
      this.formErrors = {};
      if (!this.formData.username) {
        this.formErrors.username = 'Введите имя пользователя';
      }
      if (!this.formData.public) {
        this.formErrors.public = 'Установите флажок';
      }
      if (!this.formData.email) {
        this.formErrors.email = 'Введите email';
      }
      if (!this.formData.password) {
        this.formErrors.password = 'Введите пароль';
      }
      if (this.formData.password != this.formData.password_repeat) {
        this.formErrors.passwords = 'Пароли не совпадают';
      }   
      if (Object.keys(this.formErrors).length > 0) {
        return;
      }
      setTimeout(() => {
        this.registrationSuccess = true;
        this.isSent = true;
      }, 1000);
    }
  }
};
</script>

<style scoped>
.input-container{
  position: relative;
  height: fit-content;
}
#public-error{
  width: 200px;
  top: 50px;
}
.error {
  color: red;
  position:absolute;
  top: 40px;
  left: 0;
  font-style: italic;
  margin: 0;
}
.form-window{
  display: block;
  width: 900px;
  height: 500px;
  background-color: #fff;
  border-radius: 15px;
  transition: all 1s;
}
h1{
  font-family: Montserrat;
  font-size: 19px;
  font-weight: 700;
  padding: 20px 0 5px 5%;
}
span{
  font-family: Montserrat;
  display: block;
  font-size: 16px;
  font-weight: 500;
  margin: 20px 0 20px 5%;
}
.input{
  display: flex;
  width: 90%;
  margin: 0 auto;
  justify-content: space-between;
}
.input__column{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 48%;
}
.input__column input{
  margin-bottom: 30px;
  font-family: Montserrat;
  font-size: 14px;
  font-weight: 300;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #E6E6EB;
  color: #9292A0;
  width: 100%;
  box-sizing: border-box;
}
.input__column select{
  margin-bottom: 30px;
  font-family: Montserrat;
  font-size: 14px;
  font-weight: 300;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #E6E6EB;
  color: #9292A0;
  box-sizing: border-box;
  width: 100%;
  appearance: none;
  -ms-appearance: none;
  -moz-appearance: none;
  -webkit-appearance : none;
}
.show{
  background-color: transparent;
  border: none;
  position: absolute;
  top: 12px;
  right: 10px;
  cursor: pointer;
}
.password{
  position: relative;
}
.another{
  display: block;
  width: 90%;
  margin: 20px auto 0 auto;
}
.another__input{
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
}
.switch {
  position: relative;
  display: inline-block;
  width: 36px;
  height: 20px;
  margin-right: 10px;
}

.switch input {
  display: none;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 18px;
  width: 18px;
  left: 1px;
  bottom: 1px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #3586FF;
}

input:focus + .slider {
  box-shadow: 0 0 1px #3586FF;
}

input:checked + .slider:before {
  -webkit-transform: translateX(15px);
  -ms-transform: translateX(15px);
  transform: translateX(15px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}

.another__input__text{
  margin: 0;
}

.another__text{
  font-family: Montserrat;
  font-size: 14px;
  font-weight: 400;
  margin: 0;
  color: #696977;
  margin-top: 10px;
}
.submit{
  display: flex;
  width: 90%;
  margin: 0 auto;
  justify-content: space-between;
  margin-top: 30px;
}
.submit__text{
  display: flex;
  align-items: flex-start;
  width: 68%;
}
.submit__text__input{
  margin: 0 0 0 10px;
  font-family: Montserrat;
  font-size: 14px;
  font-weight: 400;
}
.blue-text{
  display: inline;
  font-family: Montserrat;
  font-size: 14px;
  font-weight: 400;
  margin: 0;
  color: #3586FF;
  cursor: pointer;
}
.submit__button{
  border: none;
  font-family: Montserrat;
  font-size: 12px;
  font-weight: 400;
  color: #3586FF;
  border-radius: 10px;
  padding: 10px 60px;
  background-color: rgba(73, 122, 218, 0.2);
  cursor: pointer;
}
@keyframes showText{
  0%{
    opacity: 0;
  }
  100%{
    opacity: 1;
  }
}
.success{
  padding: 20px;
  width: 400px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  border-radius: 20px;
  font-family: Montserrat;
  font-size: 20px;
  font-weight: 700;
  color: black;
  background-color: #fff;
  animation: showText forwards 1s ease-in-out;
}

</style>
