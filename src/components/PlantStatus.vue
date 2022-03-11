<template>
  <div class="status">
    <div class="status__outer">
      <div class="status__animation"></div>
      <div class="status__inner">
        <div class="status__content">
          <p>{{ amount }}</p>
          <img :src="icon" :alt="`icon ${unit}`" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, defineComponent } from "vue";

export default defineComponent({
  name: "PlantStatus",
  props: {
    unit: {
      type: String,
      required: "temperature",
    },
    amount: {
      type: Number,
      default: 0,
    },
  },
  setup(props) {
    const icon = computed(() => {
      let i = "";
      switch (props.unit) {
        case "temperature":
          i = require("../assets/images/icon-temp.svg");
          break;
        case "humidity":
          i = require("../assets/images/icon-plant.svg");
          break;
        case "luminosity":
          i = require("../assets/images/icon-sun.svg");
          break;
        default:
          break;
      }
      return i;
    });
    return { icon };
  },
});
</script>

<style scoped lang="scss">
.status {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  &__outer {
    width: 283px;
    height: 283px;
    border: 27px solid #e3e6ec;
    box-sizing: border-box;
    box-shadow: inset 20px 20px 30px #d1d9e6, inset -20px -20px 30px #ffffff;
    border-radius: 1000px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }
  &__animation {
    width: 100%;
    height: 100%;
    border-radius: 1000px;
    position: absolute;
    z-index: 1;
    top: 0;
    left: 0;
    background-color: #e3e6ec;
    box-shadow: 18px 18px 50px rgba(30, 255, 228, 0.42),
      -18px -18px 60px rgba(95, 149, 255, 0.29);
    animation: spin 2s linear infinite;
  }
  &__inner {
    width: 230px;
    height: 230px;
    background: #ecf0f3;
    border-radius: 135px;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    z-index: 2;
  }
  &__content {
    display: flex;
    justify-content: center;
    align-items: center;
    p {
      margin: 0;
      padding: 0;
      font-style: normal;
      font-weight: 300;
      font-size: 42px;
      line-height: 57px;
      color: #a3a4a7;
    }
    img {
      margin-left: 20px;
      width: 35px;
    }
  }
}
@keyframes spin {
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
</style>
