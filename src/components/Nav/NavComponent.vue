<template>
  <div class="nav">
    <div class="container">
      <nav>
        <a href="#">全部商品分類</a>
        <a href="#">服裝城</a>
        <a href="#">美妝館</a>
        <a href="#">尚優選超市</a>
        <a href="#">全球購</a>
        <a href="#">閃購</a>
        <a href="#">團購</a>
        <a href="#">有趣</a>
        <a href="#">秒殺</a>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  name:'NavComponent'
}
</script>

<style lang="sass" scoped>
@mixin container($parms)
  margin: 0 auto
  width: $parms

.nav
  border-bottom : 2px solid #e1251b
  .container
    @include container(1200px)
    nav
      height: 50px
      display: flex
      align-items: center
      a
        line-height: 50px
        margin: 0 22px
        font-size: 16px
        color: #333
        &:first-child
          width: 210px
          background-color: #e1251b
          color: #fff
          font-size: 14px
          font-weight: bold
          text-align: center
</style>