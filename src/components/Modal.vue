<template>
  <div class="modal" ref="modalRef">
    <div class="modal__header">
      <div class="modal__icon"></div>
    </div>
    <div class="modal__content">
      <h3>Edit and configure</h3>
      <p>Configure the ideal preferences for your type of plant</p>
    </div>
  </div>
</template>
<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "AppModal",
  setup() {
    const modalRef = ref();
    return {
      modalRef,
    };
  },
});
</script>

<style scoped lang="scss">
.modal {
  background: #ecf0f3;
  box-shadow: 12px 12px 10px #d1d9e6, -12px -12px 20px #ffffff;
  border-radius: 65px;
  max-width: 414px;
  height: 500px;
  position: absolute;
  left: 0;
  bottom: calc(62px - 500px);
  &__header {
    padding-top: 30px;
    padding-bottom: 10px;
    text-align: center;
  }
  &__content {
    padding: 0 60px;
    h3 {
      font-family: "Noto Sans";
      font-style: normal;
      font-weight: 700;
      font-size: 24px;
      line-height: 33px;
      color: #6e7686;
    }
  }
  &__icon {
    width: 40px;
    height: 6px;
    background: #6e7686;
    border-radius: 19px;
    display: inline-block;
  }
}
</style>
