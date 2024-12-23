<template>
  <div class="wrapper">
    <h2 class="form-title">Submit a Complaint</h2>
    <ComplaintForm @submit="handleSubmit" :is-saving="isSaving" />
    <h2 class="list-title">Complaints List</h2>
    <!-- Show SkeletonScaffold while loading -->
    <SkeletonScaffold v-if="isLoading && complains.length == 0" />
    <!-- Show data or "No complaints found" message once loading is complete -->
    <ComplaintList v-else :complains="complains" />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { fetchData, postData } from "@/utils/api";
const { $toast } = useNuxtApp();
const baseUrl = "https://sugarytestapi.azurewebsites.net/";
const listPath = "TestApi/GetComplains";
const savePath = "TestApi/SaveComplain";

const complains = ref([]);
const isSaving = ref(false);
const isLoading = ref(true);

// Fetch complaints from the API
const fetchComplains = async () => {
  isLoading.value = true;
  try {
    const data = await fetchData(`${baseUrl}${listPath}`);
    complains.value = data || [];
  } catch (error) {
    $toast.error("Failed to fetch complaints. Please try again later.");
  } finally {
    isLoading.value = false;
  }
};

// Handle form submission
const handleSubmit = async ({ title, body }) => {
  isSaving.value = true;
  try {
    const response = await postData(`${baseUrl}${savePath}`, { Title: title, Body: body });
    if (response?.Success) {
      $toast.success("Complaint submitted successfully!");
      await fetchComplains(); // Refresh the list
    } else {
      $toast.error("Failed to submit complaint. Please try again.");
    }
  } catch (error) {
    $toast.error("Error occurred while submitting the complaint.");
  } finally {
    isSaving.value = false;
  }
};

onMounted(fetchComplains);
</script>
