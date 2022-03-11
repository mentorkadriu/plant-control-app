<script>
import data from "../assets/data.ts";
import { defineComponent, onMounted, ref } from "vue";
import AppModal from "@/components/Modal";

export default defineComponent({
  name: "HomeView",
  components: { AppModal },
  setup() {
    const plants = ref([]);
    function getImgUrl(image) {
      return require(`../assets/images/${image}`);
    }
    onMounted(() => {
      plants.value = data;
    });
    return {
      plants,
      getImgUrl,
    };
  },
});
</script>
<template>
  <div class="home">
    <div class="padding-h">
      <h2 class="home__title">Hello, <strong>John Doe</strong>!</h2>
      <p class="home__subtitle">Follow the growth of your plant!</p>
      <div class="info">
        <div class="info__icon">
          <img src="../assets/images/icon-plant.svg" alt="icon plant" />
        </div>
        <div class="info__growth">
          <h3>18.3 <span>Cm</span></h3>
          <p>Your plant has grown!</p>
        </div>
      </div>
    </div>
    <div class="slider">
      <div class="slider__inner">
        <div v-for="plant in plants" :key="plant.id">
          <router-link :to="`/plant/${plant.id}`">
            <div class="slider__slide">
              <img :src="getImgUrl(plant.image)" alt="icon plant" />
              <p>{{ plant.name }}</p>
            </div>
          </router-link>
        </div>
      </div>
    </div>
    <AppModal />
  </div>
</template>
<style scoped lang="scss">
@import "src/assets/scss/styles";

p,
p.phar,
.phar {
  padding: 0;
  margin: 0;
  font-weight: 500;
  font-size: 16px;
  line-height: 22px;
  color: rgba(110, 118, 134, 0.4);
}

.slider {
  padding: 50px 0;
  max-width: 414px;
  overflow: hidden;
  overflow-x: auto;
  &__inner {
    width: 1000px;
    padding-left: 90px;
    display: flex;
  }
  a {
    text-decoration: none;
  }
  &__slide {
    width: 202px;
    height: 305px;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    background: #ecf0f3;
    box-shadow: 12px 12px 10px #d1d9e6, -12px -12px 20px #ffffff;
    border-radius: 18px;
    margin-right: 42px;
    img {
      max-width: 110px;
    }
    p {
      font-weight: 700;
      font-size: 18px;
      line-height: 25px;
      color: #6e7686;
    }
  }
}

.home {
  background-color: $bg-primary;
  padding-top: 70px;
  text-align: left;
  &__title {
    font-weight: 400;
    font-size: 28px;
    line-height: 38px;
    padding: 0;
    margin: 0;
  }
  &__subtitle {
    @extend .phar;
    margin-bottom: 60px;
  }
}
.info {
  display: flex;
  align-items: center;
  &__icon {
    width: 70px;
    height: 70px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #ecf0f3;
    box-shadow: 18px 18px 20px #d1d9e6, -18px -18px 20px #ffffff;
    border-radius: 30px;
    img {
      max-width: 30px;
    }
  }
  &__growth {
    margin-left: 23px;
    h3 {
      font-weight: 400;
      font-size: 28px;
      line-height: 38px;
      color: #6e7686;
      margin: 0;
      padding: 0;
      span {
        font-size: 16px;
      }
    }
    p {
      margin: 0;
      padding: 0;
    }
  }
}
</style>
