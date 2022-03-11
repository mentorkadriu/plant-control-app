<template>
  <div class="plant">
    <router-link to="/" class="padding-h mb-40 back-button">
      <img src="../assets/images/icon-arrow-left.svg" alt="icon-arrow-left" />
    </router-link>
    <div class="padding-h mb-40">
      <h3 class="title">
        <strong>{{ plant.name }}</strong>
      </h3>
      <p class="phar">{{ plant.description }}</p>
    </div>
    <div class="actions padding-h">
      <button
        :class="[
          'action-button',
          {
            active: unit === 'temperature',
          },
        ]"
        @click="displayPlantStatus('temperature')"
      >
        <img src="../assets/images/icon-temp.svg" alt="icon temp" />
      </button>
      <button
        :class="[
          'action-button',
          {
            active: unit === 'luminosity',
          },
        ]"
        @click="displayPlantStatus('luminosity')"
      >
        <img src="../assets/images/icon-sun.svg" alt="icon sun" />
      </button>
      <button
        :class="[
          'action-button',
          {
            active: unit === 'humidity',
          },
        ]"
        @click="displayPlantStatus('humidity')"
      >
        <img src="../assets/images/icon-plant.svg" alt="icon plant" />
      </button>
    </div>
    <div class="plant__status padding-h">
      <PlantStatus :unit="unit" :amount="plant.idealConditions[unit]" />
    </div>
    <div class="plant__adjust">
      <div class="padding-h">
        <button class="button button--adjust">
          {{ adjustButtonText }}
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import data from "../assets/data";
import { computed, defineComponent, Ref, ref } from "vue";
import PlantStatus from "@/components/PlantStatus.vue";
import { UnitType } from "@/types";
import { useRoute } from "vue-router";
export default defineComponent({
  name: "PlantView",
  components: { PlantStatus },
  setup() {
    const route = useRoute();
    const unit: Ref<UnitType> = ref("temperature");
    const adjustButtonText = computed(() => {
      return `Adjust ${unit.value}`;
    });
    const plant = ref(
      data.find((plant) => plant.id === Number(route.params.id)) || data[0]
    );

    function displayPlantStatus(type: UnitType) {
      unit.value = type;
    }

    return {
      displayPlantStatus,
      unit,
      adjustButtonText,
      plant,
    };
  },
});
</script>

<style scoped lang="scss">
@import "src/assets/scss/styles";
.button {
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
  cursor: pointer;
  outline: none;
  border-radius: 12px;
  background: #ecf0f3;
  box-shadow: 12px 12px 10px #d1d9e6, -12px -12px 20px #ffffff;
  transition: all 0.4s ease-in-out;
  width: 100%;
  font-weight: 700;
  font-size: 18px;
  line-height: 25px;
  color: #6e7686;
  &--adjust {
    padding: 20px 0;
  }

  &:hover,
  &:focus {
    background: #e6e9ef;
    box-shadow: 10px 10px 8px #d1d9e6, -10px -10px 20px #ffffff;
    transition: all 0.2s ease-in-out;
  }

  &.active,
  &:active {
    box-shadow: inset 12px 12px 20px #d1d9e6, inset -12px -12px 20px #ffffff;
    transition: all 0.4s ease-in-out;
  }
}
.actions {
  display: flex;
  justify-content: space-around;
  @extend .mb-40;
}
.action-button {
  @extend .button;
  width: 56px;
  height: 54px;
}
.plant {
  background-color: $bg-primary;
  padding-top: 70px;
  text-align: left;
  height: 100%;
  display: flex;
  flex-direction: column;
  &__status {
  }
  &__adjust {
    z-index: 1;
    position: absolute;
    width: 100%;
    bottom: 43px;
    left: 0;
  }
}
.mb {
  &-40 {
    margin-bottom: 40px;
  }
}
.back-button {
  display: inline-block;
}
</style>
