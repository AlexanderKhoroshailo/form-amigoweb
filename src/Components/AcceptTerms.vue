<template>
  <div class="checkbox">
    <input
      class="custom-checkbox"
      type="checkbox"
      id="politic"
      name="politic"
      v-model="checked"
      @change="console"
    />
    <label for="politic"
      >Принимаю
      <span class="span-blue" @click.stop="alert()"> условия &nbsp;</span>
      использования
    </label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      checked: false,
    };
  },
  methods: {
    alert() {
      event.preventDefault();
      alert("Политика");
    },
    console() {
      this.$emit("politicChecked", this.checked);
    },
  },
};
</script>

<style scoped>
label {
  font-family: IBM Plex Sans;
  font-style: normal;
  font-weight: 500;
  font-size: 16px;
  line-height: 21px;
  color: #756f86;
  cursor: pointer;
}
.custom-checkbox {
  position: absolute;
  z-index: -1;
  opacity: 0;
}

/* для элемента label, связанного с .custom-checkbox */
.custom-checkbox + label {
  display: inline-flex;
  align-items: center;
  user-select: none;
}

/* создание в label псевдоэлемента before со следующими стилями */
.custom-checkbox + label::before {
  content: "";
  display: inline-block;
  height: 28px;
  width: 28px;
  flex-shrink: 0;
  flex-grow: 0;
  border: 1px solid #adb5bd;
  border-radius: 4px;
  margin-right: 10px;

  background-repeat: no-repeat;
  background-position: center center;
  background-size: 50% 50%;
}

/* стили для чекбокса, находящегося в состоянии checked */
.custom-checkbox:checked + label::before {
  border-color: #0880ae;
  background-color: #0880ae;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8 8'%3e%3cpath fill='%23fff' d='M6.564.75l-3.59 3.612-1.538-1.55L0 4.26 2.974 7.25 8 2.193z'/%3e%3c/svg%3e");
}

/* стили для чекбокса, находящегося в состоянии disabled */
.custom-checkbox:disabled + label::before {
  background-color: #e9ecef;
}
.checkbox {
  margin-bottom: 37px;
  padding-bottom: 0px;
}
</style>
