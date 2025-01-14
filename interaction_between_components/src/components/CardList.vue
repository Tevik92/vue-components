<template>
  <div class="card-list">
    <div
      v-for="card in cards"
      :key="card.id"
      class="card"
      @click="$emit('card-click', card)"
    >
      {{ card.title }}
      {{ card.description }}
    </div>
  </div>
</template>

<script>
export default {
  props: ["cards"],
};
</script>

<style scoped>
.card-list {
  display: flex;
  width: 1024px;
  flex-wrap: wrap;
  gap: 24px;
}

.card {
  width: 440px;
  padding: 16px;
  background-color: #eae9e9;
  border-radius: 12px;
  cursor: pointer;
}

.card-title {
  font: 600;
  margin-bottom: 2px;
}
</style>
