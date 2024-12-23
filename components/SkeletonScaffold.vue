<template>
  <div class="skeleton-list">
    <div class="post" v-for="index in skeletonCount" :key="index">
      <div class="avatar"></div>
      <div class="lines">
        <div class="line"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const skeletonCount = ref(8);
</script>

<style scoped>
@keyframes shine-lines {
  0% {
    background-position: -100px;
  }
  40%,
  100% {
    background-position: 140px;
  }
}
.skeleton-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.post {
  width: 100%;
  display: flex;
  align-items: flex-start;
  gap: 10px;
  margin-bottom: 15px;
}

.lines {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 90%;
}

.line {
  width: 100%;
  height: 100px;
  border-radius: 7px;
  background-image: linear-gradient(90deg, #ddd 0px, #e8e8e8 40px, #ddd 80px);
  background-size: 600px;
  animation: shine-lines 1.6s infinite linear;
}
.line ~ .line {
  background-color: #ddd;
}

.post .avatar {
  width: 50px;
  height: 50px;
  background-color: #ccc;
  border-radius: 25%;
  background-image: linear-gradient(90deg, #ddd 0px, #e8e8e8 40px, #ddd 80px);
  background-size: 600px;
  animation: shine-avatar 1.6s infinite linear;
}
</style>
