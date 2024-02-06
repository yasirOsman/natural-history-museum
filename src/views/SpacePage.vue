<template>
  <div class="space-page">
    <h1 class="space-page__title">Space</h1>

    <!-- Add the museum highlight cards based on the data provided below -->
    <div class="card-list">
      <MuseumHighlight v-for="data in highlightData" :cardData="data">
        <template v-slot:buttons>
          <a class="quiz-button" v-if="data.quiz" :href="data.quiz" target="_blank">Quiz</a>
        </template>
        <template v-slot:badge>
          <div class="card__badge">
            <font-awesome-icon :icon="['fas', 'star']" style="color: #ffd43b" size="2xl" />
          </div>
        </template>
        <!-- The extra data on the other pages can be added to the "other" slot.
        for example the "Period" key on dinosaur page and the "Location", "Species", and "Endangered status" keys on the Wildlife page, -->
      </MuseumHighlight>
    </div>
  </div>
</template>

<script>
import MuseumHighlight from '../components/MuseumHighlight.vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

export default {
  name: 'SpacePage',
  components: {
    FontAwesomeIcon,
    MuseumHighlight
  },
  mixins: [],
  props: {},
  data() {
    return {
      spaceHighlights: [
        {
          date: '2020-04-20 12:20:00',
          description:
            'Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.',
          id: 1,
          image: '',
          name: 'Asteroids'
        },
        {
          date: '2020-05-20 15:50:00',
          description:
            'A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.',
          id: 9,
          image: '',
          name: 'Comets'
        },
        {
          date: '2020-05-01 9:22:00',
          description:
            'The term planet is ancient, with ties to history, astrology, science, mythology, and religion.',
          id: 7,
          image: '',
          name: 'Planets',
          news: {
            date: '2020-08-18 18:00:00',
            title: 'Attend our talk about Jupiter with Dr. Hogarth'
          },
          quiz: 'https://planetquiz.space'
        },
        {
          date: '2020-07-05 4:10:00',
          description:
            'A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.',
          id: 12,
          image: '',
          name: 'Meteor showers',
          news: {
            title: 'The Lyrids will peak at on April 21-22 2021, at night'
          }
        }
      ],
      spacePartners: {
        observatory: {
          createdAt: '2020-06-01 11:45:00',
          info: 'The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.',
          image: '',
          name: 'Mauna Kea Observatories'
        }
      }
    }
  },
  computed: {
    highlightData() {
      let spacePartnerHighlights = []
      // create an array of the spacePartners object properties containing the highlight data
      for (const key in this.spacePartners) {
        const { createdAt, info, ...partialObject } = this.spacePartners[key]
        spacePartnerHighlights.push({
          date: createdAt,
          description: info,
          isPartner: true,
          ...partialObject
        })
      }
      return [...this.spaceHighlights, ...spacePartnerHighlights].sort((a, b) => {
        return new Date(b.date) - new Date(a.date)
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.space-page {
  &__title {
    color: #f0f0f0;
    font-size: 10rem;
    font-weight: 700;
    font-family: Arial, serif;
    margin: 5rem;
  }

  .card-list {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    gap: 3rem;
    margin: 2rem;
  }
  .quiz-button {
    display: inline-block;
    padding: 5px 20px;
    margin: 5px;
    border: 1px solid #ccc;
    border-radius: 0.25rem;
    background-color: #e0e0e0;
    color: #111;
    font-size: 16px;
    font-weight: bold;
    text-align: center;
    text-decoration: none;
    transition:
      background-color 0.3s ease,
      color 0.3s ease;
    &:hover {
      background-color: rgba(250, 250, 250, 0.1);
      color: #cccccc;
    }
  }
  .card__badge {
    transform: translate(92%, -1930%);
  }
}
</style>
