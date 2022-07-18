<template>
  <div id="app">
    <HeaderComponent />
    <NavComponent />
    <MainPage />
    <DetailPage />
    <RightNavPage
      :style="{
        top: 0 + 'px',
        right: control.arr[control.num] + 'px',
      }"
      @getControl="setControl"
    />
  </div>
</template>

<script>
import HeaderComponent from "./components/Header/HeaderComponent.vue";
import NavComponent from "./components/Nav/NavComponent.vue";
import MainPage from "./components/Main/MainPage.vue";
import DetailPage from "./components/Detail/DtailPage.vue";
import RightNavPage from "./components/RightNav/RightNavPage.vue";
export default {
  name: "App",
  components: {
    HeaderComponent,
    NavComponent,
    MainPage,
    DetailPage,
    RightNavPage,
  },
  data() {
    return {
      control: { num: 0, arr: [-294, 0] },
    };
  },
  methods: {
    setControl(val) {
      this.control.num = val;
    },
  },
};
</script>

<style lang="sass" scoped>
#app
  position: relative
</style>
