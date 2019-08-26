<template>
  <div id="app" @keypress.enter.ctrl.exact="addComment">
    <div class="wrapper">
      <section class="manager">
        <figure class="manager__avatar">
          <img src="./assets/img/manager01.png" alt="manager-photo" class="manager__image">
        </figure>
        <span class="manager__name">Вероника Ростова</span>
        <span class="manager__positions">Менджер по продажам</span>
        <p class="manager__comment">
          Подберу для вас самые лучшие предложения. Мои услуги абсолютно бесплатны.
        </p>
      </section>
      <section class="services">
        <span class="services__header">Услуг</span>
        <ul class="services__list">
          <li class="services__item" v-for="service in services" :key="service.id">
            <span class="services__name" :class="{'completed': service.qty > 10}">
              {{service.name}}
            </span>
            <span class="services__qty">{{service.qty}}</span>
          </li>
        </ul>
        <div class="services__footer">
          <span>Всего</span>
          <span>{{servicesQuantity}}</span>
        </div>
      </section>
      <section class="comments">
        <div class="comments__header">
          <div class="comments__description">
            <span class="description__text">Последние отзывы</span>
            <button class="description__button">Все отзывы</button>
          </div>
          <div class="comments__statistic">
            <div class="likes">
              <img src="./assets/img/favorite-heart.png" alt="heart" class="statistics__image">
              <span>120</span>
            </div>
            <div class="comments__qty">
              <img src="./assets/img/chat.png" alt="chat" class="statistics__image" >
              <span>{{comments.length}}</span>
            </div>
          </div>
        </div>
        <ul class="comments__list">
          <li v-for="comment in comments" :key="comment.id" class="comment__item">
            <div class="comment__header">
              <span class="comment__name">{{comment.name}}</span>
              <span class="comment__date">{{comment.date}}</span>
            </div>
            <div class="comment__body">
              {{ comment.text }}
            </div>
          </li>
        </ul>
      </section>
      <section class="form-wrapper">
        <form class="form">
          <textarea name="comment" v-model="comment" id="" cols="30" rows="4" class="form__input">
          </textarea>
          <button type="button" class="form__button" @click="addComment">
            Написать консультанту
          </button>
        </form>
      </section>
    </div>
  </div>
</template>

<style>
@import "./style.css";
</style>

<script>
import comments from './assets/mock-data/comments';
import services from './assets/mock-data/servises';

export default {
  name: 'app',
  components: {
  },
  data() {
    return {
      comment: '',
      comments,
      services,
    };
  },
  methods: {
    addComment() {
      if (this.comment.length) {
        this.comments.unshift(
          {
            id: this.comments.length + 1,
            name: 'Иван Сидоров',
            date: this.getDate,
            text: this.comment,
          },
        );
        this.comment = '';
      }
    },
  },
  computed: {
    servicesQuantity() {
      return this.services.reduce((sum, { qty }) => sum + qty, 0);
    },
    getDate() {
      return `${new Date().getDate()}
              ${new Date().toLocaleString('ru', { month: 'long' })}
              ${new Date().getFullYear()}`;
    },
  },
};
</script>
