<template>
  <div>
    <!-- NAME -->
    <div class="form-item">
      <label for="name">Имя</label>
      <input
        class="input-focus"
        type="text"
        id="name"
        placeholder="Введите Ваше имя"
        v-model="name"
        v-on:input="validateInputData(name, $options.titleOptions.namePattern)"
        required
      />
      <span v-show="validName" class="label-wrong" for="name"
        >Введено некорректное значение</span
      >
    </div>
    <!-- EMAIL -->
    <div class="form-item">
      <label for="email">Email</label>
      <input
        class="input-focus"
        id="email"
        type="email"
        placeholder="Введите ваш email"
        v-model="email"
        v-on:input="
          validateInputData(email, $options.titleOptions.emailPattern)
        "
        required
      />
      <span v-show="validEmail" class="label-wrong" for="email"
        >Введено некорректное значение</span
      >
    </div>
    <!-- PHONE -->
    <div class="form-item">
      <label for="phone">Номер телефона</label>
      <input
        class="input-focus"
        id="phone"
        type="phone"
        placeholder="Введите номер телефона"
        v-model="phone"
        v-on:input="
          validateInputData(phone, $options.titleOptions.phonePattern)
        "
        required
      />
      <span v-show="validPhone" class="label-wrong" for="phone"
        >Введено некорректное значение</span
      >
    </div>
    <!-- LANGS -->
    <div class="form-item">
      <label for="radios">Язык</label>
      <details id="custom-select">
        <summary id="radios">
          <div style="width: 100px">
            <input
              type="radio"
              class="default"
              name="item"
              id="default"
              title="Язык"
              checked
              required
            />
          </div>

          <div
            v-for="lang in $options.titleOptions.optionLangs.langs"
            :key="lang.title"
            style="width: 100px"
          >
            <input
              class="inputTitle"
              type="radio"
              name="item"
              :id="lang.title"
              :title="lang.title"
              @click="getLang()"
            />
          </div>
        </summary>
        <ul class="list">
          <li
            v-for="(lang, idx) in $options.titleOptions.optionLangs.langs"
            :key="idx"
          >
            <label class="labelLang" :for="lang.title" @click="closeDrop"
              >{{ lang.title }}
            </label>
          </li>
        </ul>
      </details>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name: "",
      phone: "",
      email: "",
      lang: "",
      validName: false,
      validEmail: false,
      validPhone: false,
      validLang: false,
    };
  },
  titleOptions: {
    namePattern: /^(([a-zA-Z' -]{2,30})|([а-яА-ЯЁё' -]{2,30}))$/u,
    emailPattern:
      /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/,
    phonePattern: /^\+?[78][-(]?\d{3}\)?-?\d{3}-?\d{2}-?\d{2}$/,

    optionLangs: {
      name: "lang",
      label: "Язык",
      placeholder: "Язык",
      type: "text",
      langs: [
        { title: "Русский" },
        { title: "Английский" },
        { title: "Китайский" },
        { title: "Испанский" },
      ],
    },
  },
  methods: {
    getLang() {
      this.lang = event.target.title;
      this.validLang = true;
    },
    validateInputData(inputData, pattern) {
      switch (event.target.id) {
        case "name":
          if (!inputData) return (this.validName = false);
          this.validName = !pattern.test(inputData);
          break;
        case "email":
          if (!inputData) return (this.validEmail = false);
          this.validEmail = !pattern.test(inputData);
          break;
        case "phone":
          if (!inputData) return (this.validPhone = false);
          this.validPhone = !pattern.test(inputData);
          break;
      }
      // console.log(
      //   "FROM VALIDATIONS name= ",
      //   this.name,
      //   " - ,",
      //   this.validName,
      //   ", email= ",
      //   this.email,
      //   " - ",
      //   this.validEmail,
      //   " phone= ",
      //   this.phone,
      //   " - ",
      //   this.validPhone,
      //   " lang= ",
      //   this.lang,
      //   " - ",
      //   this.validLang
      // );
      this.$emit(
        "getValidInputs",
        this.validLang &&
          this.lang &&
          !this.validEmail &&
          this.email &&
          !this.validPhone &&
          this.phone &&
          !this.validName &&
          this.name
      );
    },
    closeDrop() {
      const customSelect = document.getElementById("custom-select");
      customSelect.open = false;
      this.lang = event.target.innerHTML;
      this.validLang = true;

      this.$emit(
        "getValidInputs",
        this.validLang &&
          this.lang &&
          !this.validEmail &&
          this.email &&
          !this.validPhone &&
          this.phone &&
          !this.validName &&
          this.name
      );
    },
  },
};
</script>

<style scoped>
.form-item {
  display: flex;
  flex-direction: column;
  position: relative;
}
span {
  position: absolute;
  bottom: 0px;
}
label {
  font-weight: 500;
  font-size: 16px;
  line-height: 21px;
  color: #756f86;
  margin-bottom: 7px;
}
.labelLang {
  cursor: pointer;
}
input {
  width: 400px;
  height: 52px;
  background: #ffffff;
  border: 1px solid #dbe2ea;
  font-weight: normal;
  font-size: 16px;
  line-height: 21px;
  box-sizing: border-box;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
  border-radius: 6px;
  color: #2c2738;
  padding-left: 16px;
  padding-top: 16px;
  padding-bottom: 13px;
  margin-bottom: 34px;
}
.inputTitle {
  border: none;
  padding-left: 0px;
}
::placeholder {
  color: #7c9cbf;
  font-weight: normal;
  font-size: 16px;
  line-height: 21px;
}
.default {
  color: #7c9cbf;
  font-weight: normal;
  font-size: 16px;
  line-height: 21px;
  border: none;
  padding-left: 0px;
}
input:focus {
  background: #ffffff;
  border: 2px solid #0880ae;
  box-sizing: border-box;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
  border-radius: 6px;
}
.label-wrong {
  font-weight: normal;
  font-size: 14px;
  line-height: 18px;
  color: #ff7171;
  margin-top: 8px;
  margin-bottom: 8px;
}
/* --------------------------- */

body {
  background-color: #262626;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  font-family: sans-serif;
  padding: 5rem;
}

details {
  position: relative;
  width: 300px;
  margin-right: 1rem;
}

details[open] {
  z-index: 1;
}

summary {
  padding: 1rem;
  cursor: pointer;
  list-style: none;

  background: #ffffff;
  border: 1px solid #dbe2ea;
  box-sizing: border-box;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04);
  border-radius: 6px;
  width: 400px;
  height: 52px;
  margin-bottom: 34px;
}

summary::-webkit-details-marker {
  display: none;
}

details[open] summary:before {
  content: "";
  display: block;
  width: 100vw;
  height: 100vh;
  background: transparent;
  position: fixed;
  top: 0;
  left: 0;
}

summary:after {
  content: "";
  position: absolute;
  top: 20px;
  display: inline-block;
  width: 10px;
  height: 10px;
  border-bottom: 3px solid currentColor;
  border-left: 3px solid currentColor;
  border-bottom-left-radius: 3px;
  transform: rotate(-45deg) translate(50%, 0%);
  transform-origin: center center;
  color: #0880ae;
  margin-left: calc(100% + 2.5rem);
}

summary:focus {
  outline: none;
}

ul {
  width: 400px;
  height: 200px;
  padding-left: 16px;
  position: absolute;
  top: calc(100% - 1.5rem);
  left: 0;
  margin: 0;
  max-height: 200px;
  overflow-y: auto;
  background: #ffffff;
  border: 1px solid #dbe2ea;
  box-sizing: border-box;
  box-shadow: 0px 4px 8px rgba(44, 39, 56, 0.04),
    0px 20px 20px rgba(44, 39, 56, 0.04);
  border-radius: 6px;
}
ul::-webkit-scrollbar {
  width: 0 !important;
}
li {
  margin: 23px 0 23px 0;
  list-style-type: none;
}

li:first-child {
  padding-top: 0;
}

li:last-child {
  padding-bottom: 0;
  border-bottom: none;
}

summary.radios {
  counter-reset: radios;
}

input[type="radio"] {
  counter-increment: radios;
  appearance: none;
  display: none;
}

input[type="radio"]:checked {
  display: inline;
}

input[type="radio"]:after {
  content: attr(title);
  display: inline;
  font-size: 1rem;
}

ul.list {
  counter-reset: labels;
}

label {
  width: 100%;
  display: block;
}
</style>
