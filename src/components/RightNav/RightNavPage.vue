<template>
  <div class="container">
    <div class="right-nav" ref="nav">
      <div
        class="btn"
        @click="switchNav"
        :style="{ 'background-image': `url('${imgUrl[imgSwitch]}')` }"
      ></div>
      <div class="content"></div>
      <div class="nav">
        <ul>
          <li v-for="index in 6" :key="index">
            <p></p>
            <i>尚选会员</i>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "RightNavPage",
  data() {
    return {
      imgUrl: ["images/list.png", "images/cross.png"],
      imgSwitch: 0,
    };
  },
  methods: {
    switchNav() {
      if (this.imgSwitch == 0) {
        this.imgSwitch = 1;
      } else {
        this.imgSwitch = 0;
      }
      this.$emit("getControl", this.imgSwitch);
    },
  },
};
</script>

<style lang="sass" scoped>
.container
  height: 100%
  position: fixed
  transition: .5s
  .right-nav
    height: 100%
    width: 300px
    background-color: #7a6e6e
    .btn
      position: absolute
      width: 35px
      background-color: #7a6e6e
      height: 35px
      border-radius: 3px 0 0 3px
      left: -29px
      background-size: 35px 35px
      background-image: url(../../assets/toolbars.png)
    .content
      width: 294px
      height: 100%
      position: absolute
      left: 6px
      background-color: bisque
      z-index: 1
    .nav
      position: absolute
      left: -29px
      top: 50%
      transform: translateY(-50%)
      >ul
        >li
          position: relative
          >p
            height: 35px
            width: 35px
            background-color: #7a6e6e
            background-image: url(../../assets/toolbars.png)
            left: -29px
            background-position: -87px -174px
            transition: .5s
          >i
            width: 62px
            height: 35px
            text-align: center
            line-height: 35px
            position: absolute
            left: 35px
            top: 0
            transition: .5s
            background-color: #7a6e6e
          &:hover
            >p
              background-color: pink
            >i
              background-color: pink
              left: -62px
</style>