<template>
  <div>
    <h1>Регистрация</h1>
    <p>Уже есть аккаунт?<span class="span-blue" @click="alert">Войти</span></p>
  </div>
</template>

<script>
export default {
  methods: {
    alert() {
      alert("Открытие формы авторизации");
    },
  },
};
</script>

<style scoped>
div {
  margin-bottom: 58px;
}
h1 {
  font-weight: bold;
  font-size: 34px;
  line-height: 44px;
  width: 400px;
  color: #2c2738;
  margin-top: 0px;
  margin-bottom: 0px;
}
p {
  font-weight: normal;
  font-size: 16px;
  line-height: 22px;
  color: #2c2738;
  margin-top: 8px;
  margin-bottom: 0px;
}
</style>
