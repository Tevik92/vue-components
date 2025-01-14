<template>
  <div>
    <div v-if="isLoading">Loading...</div>
    <div v-else>
      <CardList :cards="cards" @card-click="handleCardClick" />
    </div>
    <CardFormModal
      v-if="cardModalIsOpen"
      :card="cardForEdit"
      @update-card="updateCard"
      @close-modal="closeModal"
    />
  </div>
</template>

<script>
import CardList from "./components/CardList.vue";
import CardFormModal from "./components/CardFormModal.vue";

export default {
  components: { CardList, CardFormModal },
  data() {
    return {
      cards: [],
      cardForEdit: null,
      cardModalIsOpen: false,
      isLoading: false,
    };
  },
  methods: {
    loadCards() {
      this.isLoading = true;
      setTimeout(() => {
        this.cards = [
          {
            id: 1,
            title: "Профессия Python-разработчик",
            description:
              "На Python пишут сайты, приложения, игры и чат-боты. Netflix, Spotify, Google, Dropbox и Youtube написаны на Python.",
          },
          {
            id: 2,
            title: "Профессия Графический дизайнер",
            description:
              "Научим делать бренды узнаваемыми через создание логотипов, графики для рекламы, упаковки и не только.",
          },
          {
            id: 3,
            title: "Профессия Инженер по тестированию",
            description:
              "Вы научитесь находить ошибки в работе сайтов и приложений с помощью Java, JavaScript или Python. С первого занятия погрузитесь в практику и сможете начать зарабатывать уже через 4 месяца.",
          },
          {
            id: 4,
            title: "Профессия Веб-разработчик",
            description:
              "Веб-разработчик создаёт сайты, сервисы и приложения, которыми мы ежедневно пользуемся. Он разрабатывает интернет-магазины, онлайн-банки, поисковики, карты и почтовые клиенты.",
          },
        ];
        this.isLoading = false;
      }, 2000);
    },
    handleCardClick(card) {
      this.cardForEdit = { ...card };
      this.cardModalIsOpen = true;
    },
    closeModal() {
      this.cardModalIsOpen = false;
    },
    updateCard(updatedCard) {
      this.isLoading = true;
      setTimeout(() => {
        this.cards = this.cards.map((card) =>
          card.id === updatedCard.id ? updatedCard : card
        );
        this.isLoading = false;
        this.closeModal();
      }, 2000);
    },
  },
  mounted() {
    this.loadCards();
  },
};
</script>

<style>
@import "@/assets/global.css";
</style>
