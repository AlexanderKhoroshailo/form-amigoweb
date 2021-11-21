<template>
  <div>
    <button
      id="submitBtn"
      type="submit"
      @click.prevent="sendForm"
      :disabled="!(activeBtn.inputValid && activeBtn.politicValid)"
    >
      <span>Зарегистрироваться</span>
    </button>
  </div>
</template>

<script>
export default {
  props: ["activeBtn"],
  data() {
    return {};
  },
  methods: {
    sendForm() {
      alert("Отправка формы");
    },
  },
};
</script>

<style>
button:not(disabled) {
  width: 400px;
  height: 56px;
  background: #0880ae;
  box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
    0px 4px 8px rgba(44, 39, 56, 0.08);
  border: 0px solid #0880ae;
  border-radius: 6px;
  margin-top: 0px;
  margin-bottom: 40px;
  padding: 0;
  cursor: pointer;
}
button:disabled {
  width: 400px;
  height: 56px;
  background: #dbe2ea;
  box-shadow: 0px 2px 4px rgba(44, 39, 56, 0.08),
    0px 4px 8px rgba(44, 39, 56, 0.08);
  border-radius: 6px;
  margin-top: 0px;
  margin-bottom: 40px;
  padding: 0;
  cursor: text;
}
button:disabled span {
  color: #b1b5bf;
}
span {
  font-family: IBM Plex Sans;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 21px;
  text-align: center;
  color: #ebf4f8;
}
</style>
