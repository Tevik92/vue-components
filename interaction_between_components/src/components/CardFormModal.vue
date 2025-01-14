<template>
  <div class="modal-overlay" @click="$emit('close-modal')">
    <div class="modal" @click.stop>
      <button class="close-btn" @click="$emit('close-modal')">×</button>
      <h2>Редактирование курса</h2>
      <label for="title">Название курса:</label>
      <input
        id="title"
        v-model="editedCard.title"
        placeholder="Введите название"
      />
      <label for="description">Описание курса:</label>
      <textarea
        id="description"
        v-model="editedCard.description"
        placeholder="Введите описание"
      ></textarea>
      <div class="modal-actions">
        <button class="save-btn" @click="saveChanges">Сохранить</button>
        <button class="cancel-btn" @click="$emit('close-modal')">
          Отменить
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["card"],
  data() {
    return {
      editedCard: { ...this.card },
    };
  },
  methods: {
    saveChanges() {
      this.$emit("update-card", this.editedCard);
    },
  },
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  width: 400px;
  max-width: 90%;
  position: relative;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
  text-align: center;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
}

input,
textarea {
  display: block;
  width: 100%;
  margin: 10px 0;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
}

.modal-actions {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
}

.save-btn {
  background-color: #28a745;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.save-btn:hover {
  background-color: #218838;
}

.cancel-btn {
  background-color: #ccc;
  color: black;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.cancel-btn:hover {
  background-color: #bbb;
}
</style>
