<template>
  <div class="museum-highlight">
    <!-- Display the available information for the highlight -->
    <div class="card" :class="{ 'card-partner': cardData.isPartner }">
      <div class="card__image">
        <img :src="`src/assets/images/${imageName.toLowerCase()}/${currentImage}.jpg`" />
        <div class="card__image__title">
          {{ cardData.name }}
        </div>
        <div class="card__image__loading" v-if="loading">
          <font-awesome-icon
            :icon="['fas', 'spinner']"
            spin-pulse
            size="2xl"
            style="color: #cccccc"
          />
        </div>
      </div>
      <div class="card__content">
        <div class="card__description">
          {{ cardData.description }}
        </div>
        <div class="card__news" v-if="cardData.news">
          <div class="card__news__title">News</div>
          <div class="card__news__body">
            {{ cardData.news.title }}
          </div>
        </div>
        <!--  slot for any other data  -->
        <div class="card__other">
          <slot name="other" />
        </div>
        <div class="card__buttons">
          <!--  slot for any extra buttons-->
          <slot name="buttons" />
          <a class="card__buttons__refresh" @click="fetchImage()">Refresh Image</a>
        </div>
      </div>
      <slot name="badge" />
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

export default {
  name: 'MuseumHighlight',
  components: {
    FontAwesomeIcon
  },
  mixins: [],
  props: {
    cardData: {
      type: Array
    }
  },
  data() {
    return {
      imageName: null,
      currentImage: 1,
      loading: false
    }
  },
  methods: {
    async fetchImage() {
      this.loading = true
      setTimeout(() => {
        if (this.currentImage >= 2) {
          this.currentImage = 1
        } else {
          this.currentImage++
        }
        this.loading = false
      }, 1000)
    }
  },
  created() {
    this.imageName = this.cardData.name.split(' ').join('_')
  }
}
</script>

<style lang="scss" scoped>
.museum-highlight {
  .card {
    width: 20rem;
    height: 40rem;
    border-radius: 0.5rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease;
    position: relative;
    display: flex;
    flex-direction: column;
    background: rgba(200, 100, 104, 0.12);

    &__image {
      height: 18rem;
      border-radius: 0.5rem 0.5rem 0 0;
      position: relative;

      img {
        width: 100%;
        height: inherit;
        border-radius: inherit;
      }

      &__title {
        margin: 0.5rem;
        font-size: 1.25rem;
        font-weight: 700;
        font-family: Arial, serif;
        color: #cccccc;
        transform: translateY(-200%);
      }
      &__loading {
        transform: translate(40%, -600%);
      }
    }

    &:hover {
      transform: translateY(-5px);
    }

    &__content {
      flex: 1;
      display: flex;
      flex-direction: column;
      color: #cccccc;
      line-height: 180%;
      font-family: 'Arial', serif;
      margin: 0.5rem;

      .card__news {
        border-top: 1px solid #6b6a6a;
        margin-top: 0.5rem;

        &__title {
          font-size: 1.1rem;
          font-weight: 700;
          margin-bottom: 5px;
        }

        &__body {
          font-size: 1rem;
        }
      }

      .card__buttons {
        display: flex;
        justify-content: space-evenly;
        margin: auto 0 1rem;

        &__refresh {
          padding: 5px 20px;
          margin: 5px;
          border: 1px solid #ccc;
          border-radius: 4px;
          background-color: rgba(250, 250, 250, 0.1);
          color: #cccccc;
          font-size: 16px;
          font-weight: bold;
          text-align: center;
          text-decoration: none;
          transition:
            background-color 0.3s ease,
            color 0.3s ease;
          cursor: pointer;

          &:hover {
            background-color: #e0e0e0;
            color: #111;
          }
        }
      }
    }
  }

  .card-partner {
    background: rgba(55, 200, 155, 0.1);
  }
}
</style>
