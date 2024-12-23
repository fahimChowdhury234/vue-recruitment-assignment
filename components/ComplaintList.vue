<template>
  <div v-if="complains.length > 0">
    <div v-for="complain in complains" :key="complain.Id" class="timeline">
      <div class="timeline-icon">
        <svg width="19" height="17" viewBox="0 0 19 17" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M15.7258 0H2.50662C1.1245 0 0 1.12428 0 2.50662V10.5965C0 11.9757 1.11961 13.0982 2.49772 13.1031V16.7742L7.77348 13.1031H15.7258C17.1079 13.1031 18.2324 11.9786 18.2324 10.5965V2.50662C18.2324 1.12428 17.1079 0 15.7258 0V0ZM17.1641 10.5965C17.1641 11.3895 16.5189 12.0348 15.7258 12.0348H7.4383L3.56603 14.7294V12.0348H2.50662C1.71352 12.0348 1.06831 11.3895 1.06831 10.5965V2.50662C1.06831 1.7134 1.71352 1.0683 2.50662 1.0683H15.7258C16.5189 1.0683 17.1641 1.7134 17.1641 2.50662V10.5965Z" fill="#999" />
          <path d="M4.88086 3.77478H13.3537V4.84308H4.88086V3.77478Z" fill="#999" />
          <path d="M4.88086 6.05383H13.3537V7.12214H4.88086V6.05383Z" fill="#999" />
          <path d="M4.88086 8.33289H13.3537V9.40121H4.88086V8.33289Z" fill="#999" />
        </svg>
      </div>
      <div class="timeline-body">
        <h3 class="complain-title">{{ complain.Title }}</h3>
        <p class="complain-body">{{ complain.Body }}</p>
      </div>
    </div>
  </div>
  <div v-else class="no-complaints-text">
    <img src="../assets/img/no-result.png" alt="no result" />
    <span>No complaints found.</span>
  </div>
</template>

<script setup>
const props = defineProps({ complains: Array });
</script>
