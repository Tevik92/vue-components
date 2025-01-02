<template>
  <div class="card-list">
    <div
      v-for="card in cards"
      :key="card.id"
      class="card"
      @click="click(isModal, card)"
    >
      <h3 class="card-title">
        {{ card.title }}
      </h3>
      <div class="card-description">
        {{ card.description }}
      </div>
    </div>
  </div>
</template>

<script setup>
const isModal = true;
const props = defineProps({
  cards: {
    type: Array,
  },
});

const emit = defineEmits(["openModal", "cardRed"]);
const click = (value, card) => {
  emit("openModal", value);
  emit("cardRed", card);
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
</style>
