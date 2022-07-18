<template>
  <div class="container">
    <div class="aside">
      <aside>
        <div class="recommend-top">
          <h4
            :class="recommend == true ? 'active' : ''"
            @click="recommend = true"
          >
            相關分類
          </h4>
          <h4
            :class="recommend == false ? 'active' : ''"
            @click="recommend = false"
          >
            推薦品牌
          </h4>
        </div>
        <div class="recommend-bottom" v-if="recommend">
          <div class="content">
            <ul>
              <li>手機</li>
              <li>手機殼</li>
              <li>內存卡</li>
              <li>iphone配件</li>
              <li>貼膜</li>
              <li>手機耳機</li>
              <li>移動電源</li>
              <li>平板電腦</li>
            </ul>
          </div>
          <div class="content-img" v-for="index in 4" :key="index">
            <img src="@/assets/part01.png" alt="part" />
            <span>Apple苹果iPhone 6s (A1699)</span>
            <p>¥6088.00</p>
            <div class="btn">
              <a href="javascript:;">加入購物車</a>
            </div>
          </div>
        </div>
        <div class="recommend-bottom" v-else>推荐品牌内容</div>
      </aside>
    </div>
    <div class="other-all">
      <div class="other-choose">
        <div class="title"><h4>選擇搭配</h4></div>
        <div class="other">
          <div class="other-item">
            <div class="img">
              <div class="item">
                <img src="@/assets/l-m01.png" alt="img-1" />
                <p>¥{{ price }}</p>
              </div>
              <i>+</i>
            </div>
            <ul>
              <li v-for="index in 4" :key="index">
                <img :src="require(`@/assets/dp0${index}.png`)" :alt="`dp0${index}`" />
                <p>Feless费勒斯VR</p>
                <input type="checkbox" :value="50 * index" v-model="otherBuy" />
                <span>{{ 50 * index }}</span>
              </li>
            </ul>
          </div>
          <div class="other-shooping">
            <p>已购{{ otherBuy.length }}件商品</p>
            <p>套餐价</p>
            <p>¥{{ totalprice }}</p>
            <button>加入購物車</button>
          </div>
        </div>
        <div class="detail">
          <div class="detail-top">
            <ul>
              <li
                v-for="(detail, index) in detailList"
                :class="detailListActive === index ? 'active' : ''"
                :key="index"
              >
                <a href="javascript:;" @click="detailListActive = index">{{
                  detail
                }}</a>
              </li>
            </ul>
          </div>
          <div class="detail-bottom">
            <div
              class="introduce"
              v-for="(detail, index) in detailList"
              v-show="index === detailListActive"
              :key="index"
            >
              <h3>{{ detail }}</h3>
              <ul>
                <li>分辨率：1920*1080(FHD)</li>
                <li>后置摄像头：1200万像素</li>
                <li>前置摄像头：500万像素</li>
                <li>核 数：其他</li>
                <li>频 率：以官网信息为准</li>
                <li>品牌： Apple</li>
                <li>商品名称：APPLEiPhone 6s Plus</li>
                <li>商品编号：1861098</li>
                <li>商品产地：中国大陆</li>
                <li>商品毛重：0.51kg</li>
                <li>热点：指纹识别，Apple Pay，金属机身，拍照神器</li>
                <li>系统：苹果（IOS）</li>
                <li>像素：1000-1600万品毛重：0.51kg</li>
                <li>机身内存：64GB</li>
              </ul>
              <img src="@/assets/intro01.png" alt="" />
              <img src="@/assets/intro02.png" alt="" />
              <img src="@/assets/intro03.png" alt="" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DetailPage",
  data() {
    return {
      detailListActive: 0,
      detailList: [
        "商品介绍",
        "规格包装",
        "售后与保障",
        "商品评价",
        "手机社区",
      ],
      recommend: true,
      price: 0,
      otherBuy: [],
    };
  },
  computed: {
    totalprice() {
      let other = this.otherBuy.reduce((a, b) => a + b, 0);
      return other + this.price;
    },
  },
  beforeMount() {
    this.$bus.$on("price", (data) => {
      this.price = data;
    });
  },
};
</script>

<style lang="sass" scoped>
.container
  width: 1200px
  margin: 30px auto 0px
  display: flex
  .aside
    height: 870px
    width: 210px
    border: 1px solid #ccc
    >aside
      .recommend-top
        display: flex
        >h4
          height: 40px
          line-height: 40px
          text-align: center
          width: 105px
          border-top: 3px solid #fff
          border-bottom: 1px solid #ccc
          &.active
            border-bottom: none
            border-top: 3px solid #e1251b
      .recommend-bottom
        padding: 10px
        margin-top: 5px
        .content
          >ul
            display: flex
            flex-wrap: wrap
            >li
              width: 50%
              border-bottom: 1px dashed #ededed
              line-height: 28px
        .content-img
          border-bottom: 1px solid #ededed
          &:last-child
            margin-bottom: 15px
          >img
            width: 152px
          >span
          >p
            font-size: 16px
            color: #c81623
          .btn
            margin: 5px 0px
            text-align: center
            >a
              line-height: 18px
              color: #8c8c8c
              padding: 2px 14px
              border: 1px solid #8c8c8c
  .other-all
    width: 980px
    margin-bottom: 15px
    margin-left: 8px
    .other-choose
      .title
        background-color: #f1f1f1
        padding: 5px 0px 5px 15px
        border: 1px solid #ddd
        border-bottom: none
        >h4
          color: #333
      .other
        display: flex
        height: 170px
        padding-top: 10px
        border: 1px solid #ddd
        .other-item
          display: flex
          .img
            width: 127px
            height: 165px
            position: relative
            .item
              >img
                width: 87px
                margin: 0 auto
              >p
                text-align: center
                color: #c81623
                font-size: 16px
            >i
              position: absolute
              top: 48px
              right: -25px
              font-size: 16px
          >ul
            display: flex
            >li
              width: 127px
              margin: 0px 20px
              text-align: center
              >img
                width: 120px
                height: 130px
              >p
              >input
                margin-right: 2px
              >span

        .other-shooping
          border-left: 1px solid #ddd
          width: 153px
          height: 165px
          padding-left: 20px
          >p
            &:first-child
              margin: 10px 0px
            &:nth-child(2)
              font-weight: bold
              margin-bottom: 10px
            &:nth-child(3)
              color: #b1191a
              font-size: 16px
              margin-bottom: 10px
          >button
            padding: 10px 25px
            font-size: 16px
            color: #fff
            background-color: #e1251b
            border: none
      .detail
        margin-top: 15px
        .detail-top
          background-color: #ededed
          >ul
            border: 1px solid #ddd
            display: flex
            >li
              background-color: #fff
              height: 40px
              padding: 0px 11px
              border-right: 1px solid #ddd
              >a
                line-height: 40px
              &.active
                background-color: red
                >a
                  color: #fff
        .detail-bottom
          .introduce
            padding-left: 20px
            line-height: 25px
            margin: 10px 0px
            &.active

            >ul
              >li
            >img
</style>