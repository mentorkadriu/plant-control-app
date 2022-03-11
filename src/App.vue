<template>
  <router-view v-slot="{ Component }">
    <transition name="fade" mode="out-in">
      <component :is="Component" />
    </transition>
  </router-view>
</template>

<style lang="scss">
@import "assets/scss/variables";
*:before,
*:after {
  box-sizing: border-box;
}

html,
body {
  font-size: 16px;
  font-family: "Noto Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $text-primary;
  background-color: $bg-primary;
  padding: 0;
  margin: 0;
  height: 100%;
}
body {
  display: flex;
  justify-content: center;
  align-items: center;
}
#app {
  max-width: 414px;
  margin: 0 auto;
  height: 100vh;
  position: relative;
  overflow: hidden;
  background: #ecf0f3;
  @media (min-width: 1024px) {
    box-shadow: 12px 42px 52px rgb(86 86 86 / 22%);
    border-radius: 58px;
    max-height: 850px;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
