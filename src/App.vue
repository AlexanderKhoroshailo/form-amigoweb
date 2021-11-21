<template>
  <div id="app">
    <div id="container">
      <AccountAvailability />
      <form id="form" action="">
        <InputData @getValidInputs="getValidInputs" />
        <AcceptTerms @politicChecked="politicChecked" />
        <SubmitForm :activeBtn="{ inputValid, politicValid }" />
      </form>
    </div>
  </div>
</template>

<script>
import AccountAvailability from "./Components/AccountAvailability.vue";
import InputData from "./Components/InputData.vue";
import AcceptTerms from "./Components/AcceptTerms.vue";
import SubmitForm from "./Components/SubmitForm.vue";
export default {
  name: "App",

  components: {
    AccountAvailability,
    InputData,
    AcceptTerms,
    SubmitForm,
  },
  data() {
    return {
      inputValid: false,
      politicValid: false,
    };
  },
  methods: {
    getValidInputs(data) {
      console.log("inputValid=", data);
      this.inputValid = data;
    },
    politicChecked(data) {
      console.log("politicValid=", data);
      this.politicValid = data;
    },
  },
};
</script>

<style>
body {
  background: black;
}
#app {
  font-family: "IBM Plex Sans";
  font-style: normal;
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  width: 460px;
  height: 789px;
  background: #ffffff;
  box-shadow: 0px 12px 24px rgba(44, 39, 56, 0.02),
    0px 32px 64px rgba(44, 39, 56, 0.04);
  border-radius: 24px;
}
#container {
  margin: 40px 30px 40px 30px;
}
#form {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.span-blue {
  margin-left: 6px;
  color: #0880ae;
}
.span-blue:hover {
  cursor: pointer;
}
</style>
