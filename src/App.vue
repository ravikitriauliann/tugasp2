<script setup>
import { ref, computed } from "vue";

const inputValue = ref("");
const items = ref([]);

const inputClasses = computed(() => {
  return {
    error: !inputValue.value,
  };
});

const inputStyles = computed(() => {
  return {
    borderColor: inputValue.value ? "green" : "red",
  };
});

const buttonClasses = computed(() => {
  return {
    success: inputValue.value,
  };
});

const buttonStyles = computed(() => {
  return {
    backgroundColor: inputValue.value ? "green" : "gray",
  };
});

const outerClasses = computed(() => {
  return {
    container: true,
    error: !inputValue.value,
  };
});

const outerStyles = computed(() => {
  return {
    border: inputValue.value ? "1px solid green" : "1px solid red",
  };
});

const updateInput = (event) => {
  inputValue.value = event.target.value;
};

const submitForm = () => {
  if (inputValue.value) {
    items.value.push(inputValue.value);
    inputValue.value = "";
  }
};
</script>

<template>
  <div :class="outerClasses" :style="outerStyles">
    <form @submit.prevent="submitForm">
      <input
        type="text"
        v-model="inputValue"
        :class="inputClasses"
        :style="inputStyles"
        @input="updateInput"
      />
      <button
        :class="buttonClasses"
        :style="buttonStyles"
        :disabled="!inputValue"
      >
        Submit
      </button>
    </form>
    <ul>
      <li v-for="item in items" :key="item">{{ item }}</li>
    </ul>
    <p>
      You have entered "<span :class="inputClasses" :style="inputStyles">{{
        inputValue
      }}</span
      >"
    </p>
  </div>
</template>

<style scoped>
.container {
  border: 1px solid red;
  padding: 10px;
  margin-bottom: 10px;
}

.error {
  border: 1px solid red;
}

.success {
  background-color: green;
}

input[type="text"] {
  width: 100%;
}

button {
  background-color: #3498db;
  padding: 10px 20px;
  margin-top: 10px;
  border: none;
  color: white;
}

.error {
  border: 1px solid red;
}

.input-value {
  font-weight: bold;
}
span {
  background-color: #3498db;
}
li {
  color: green;
}
</style>
