<template>
  <app-modal
    :model-value="isOpen"
    @update:model-value="emit('update:isOpen', $event)"
  >
    <div class="modal-wrapper">
      <h2>Редактирование курса</h2>
      <form class="form" @submit.prevent="updateCards">
        <label>
          <div>Название курса:</div>
          <input v-model="form.title" type="text" />
        </label>
        <label>
          <div>Описание курса:</div>
          <input v-model="form.description" type="text" />
        </label>
        <div class="actions">
          <button type="submit" class="save-button">Сохранить</button>
          <button @click="closeModal">Отменить</button>
        </div>
      </form>
    </div>
  </app-modal>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  isOpen: Boolean,
  card: Object,
});

const emit = defineEmits(["update:isOpen", "cardUpdate"]);

const form = ref({ ...props.card });

watch(
  () => props.card,
  (newCard) => {
    form.value = { ...newCard };
  },
  { immediate: true }
);

const updateCards = () => {
  emit("cardUpdate", { ...form.value });
};

const closeModal = () => {
  emit("update:isOpen", false);
};
</script>

<style scoped>
.modal-wrapper {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 380px;
  height: 280px;
}

.form {
  display: flex;
  align-items: center;
  flex-direction: column;
  margin-top: 16px;
}

input {
  margin-left: 4px;
  margin-bottom: 24px;
}

button {
  width: 180px;
  cursor: pointer;
}

.actions {
  display: flex;
  margin-top: 32px;
}

.save-button {
  background-color: #a2ffa2;
  margin-right: 8px;
}
</style>
