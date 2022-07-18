<template>
  <div class="header">
    <div class="header-top">
      <div class="container">
        <div class="right">
          <h5>歡迎來到尚優選！ 請</h5>
          <p>
            <a href="＃">登入</a>
            <a href="＃">註冊</a>
          </p>
        </div>
        <div class="left">
          <nav>
            <a href="#">我的訂單</a>
            <a href="#">我的購物車</a>
            <a href="#">我的尚優選</a>
            <a href="#">尚優選會員</a>
            <a href="#">企業採購</a>
            <a href="#">關注尚優選</a>
            <a href="#">合作招商</a>
            <a href="#">商家後台</a>
          </nav>
        </div>
      </div>
    </div>
    <div class="header-bottom">
      <div class="container">
        <div class="logo">
          <a href="#"><img src="@/assets/logo.png" alt="logo" /></a>
        </div>
        <div class="search">
          <input type="text" placeholder="請輸入搜尋內容" />
          <input type="button" value="搜尋" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HeaderComponent",
};
</script>

<style lang="sass" scoped>
@mixin container($parms)
  margin: 0 auto
  width: $parms

.header
  position: relative
  .RightNavPage
    border: 1px solid red
    position: absolute
    left: 0px
    top: 100px

  .header-top
    background-color: #eaeaea
    .container
      @include container(1200px)
      height: 30px
      display: flex
      justify-content: space-between
      align-items: center
      .right
        display: flex
        h5
          margin-right: 5px
        p
          a:first-child
            font-size: 12px
            border-right: 1px solid #b3aeae
            margin-right: 5px
            padding-right: 5px
      .left
        nav
          display: flex
          font-size: 0
          a
            margin-right: 10px
            padding-right: 10px
            font-size: 12px
            border-right: 1px solid #b3aeae
            &:last-child
              border: none
              margin-right: 0
              padding-right: 0
  .header-bottom
    display: flex
    .container
      @include container(1200px)
      display: flex
      justify-content: space-between
      .logo
        a
          font-size: 0px
          img
            margin: 25px 45px
            width: 175px
            height: 56px
      .search
        margin-top: 35px
        display: flex
        input
          height: 32px
          &:first-child
            box-sizing: border-box
            width: 490px
            padding: 0px 4px
            border: 3px solid #ea4a36
          &:last-child
            width: 68px
            background-color: #ea4a36
            color: #fff
            border: none
</style>