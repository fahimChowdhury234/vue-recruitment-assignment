<template>
  <form @submit.prevent="validateAndSubmit" class="complain-form">
    <input v-model="title" type="text" placeholder="Enter complaint title" class="form-input" />
    <p v-if="errors.title" class="error-text">{{ errors.title }}</p>

    <textarea v-model="body" placeholder="Describe your complaint" rows="5" class="form-textarea"></textarea>
    <p v-if="errors.body" class="error-text">{{ errors.body }}</p>

    <button :disabled="isSaving" class="form-button">
      {{ isSaving ? "Submitting..." : "Submit Complaint" }}
      <svg v-if="isSaving" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="margin: auto; background: none; display: block; shape-rendering: auto" width="25px" height="25px" viewBox="0 0 100 100" preserveAspectRatio="xMidYMid">
        <path d="M10 50A40 40 0 0 0 90 50A40 42 0 0 1 10 50" fill="#fff" stroke="none">
          <animateTransform attributeName="transform" type="rotate" dur="1s" repeatCount="indefinite" keyTimes="0;1" values="0 50 51;360 50 51"></animateTransform>
        </path>
      </svg>
    </button>
  </form>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({ isSaving: Boolean });
const emit = defineEmits(["submit"]);

const title = ref("");
const body = ref("");
const errors = ref({});

const validateAndSubmit = () => {
  errors.value = {};
  if (!title.value.trim()) errors.value.title = "Title is required.";
  if (!body.value.trim()) errors.value.body = "Description is required.";

  if (!Object.keys(errors.value).length) {
    emit("submit", { title: title.value, body: body.value });
    title.value = "";
    body.value = "";
  }
};
</script>
