<template>
  <div class="wrapper">
    <div class="container">
      <h2>Список курсов</h2>

      <CardList
        v-if="!cardsIsLoading"
        :cards="cards"
        @openModal="modalOpen"
        @cardRed="cardRed"
      />
      <p v-else>Loading...</p>
    </div>

    <CardFormModal
      :card="card"
      :is-open="cardModalIsOpen"
      @update:is-open="updateCardModal"
      @cardUpdate="updateCard"
      @click="isClosed"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import CardList from "@/components/CardList.vue";
import CardFormModal from "@/components/CardFormModal.vue";

const modalOpen = (value) => {
  cardModalIsOpen.value = value;
};

const card = ref({});

const cardRed = (el) => {
  card.value[i] = el;
};

const isClosed = () => {
  cardsIsLoading.value = true;
  cardModalIsOpen.value = false;
  setTimeout(() => {
    cardsIsLoading.value = false;
  }, 2000);
};

const cardModalIsOpen = ref(false);

const updateCardModal = (value) => {
  cardModalIsOpen.value = value;
};

const cards = ref([]);

const cardsIsLoading = ref(false);

const loadCards = () => {
  cardsIsLoading.value = true;
  setTimeout(() => {
    cards.value = [
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
    cardsIsLoading.value = false;
  }, 2000);
};

loadCards();
</script>

<style>
@import "@/assets/global.css";
</style>
