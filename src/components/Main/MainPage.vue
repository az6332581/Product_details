<template>
  <div class="container">
    <div class="nav">
      <div v-for="(data, index) in path" :key="index">
        <a href="#">{{ data.title }}</a>
        <i>/</i>
      </div>
    </div>
    <div class="content">
      <div class="content-left">
        <div class="left-top">
          <div class="small-img" ref="smallImg">
            <img
              :src="smallImgSrc"
              alt="samll"
              @mouseenter="show = true"
              @mouseleave="show = false"
              @mousemove="MouseMove($event)"
            />
            <div
              v-show="show"
              ref="mask"
              class="mask"
              :style="{
                top: mask_top + 'px',
                left: mask_left + 'px',
              }"
            ></div>
          </div>
          <div class="big-img" v-show="show">
            <div class="big">
              <img
                :src="bigImgSrc"
                alt="big"
                :style="{
                  top: -(mask_top / 0.5) + 'px',
                  left: -(mask_left / 0.5) + 'px',
                }"
              />
            </div>
          </div>
        </div>
        <div class="left-bottom">
          <a href="javascript:;" @click="prev">＜</a>
          <div class="imglist">
            <ul :style="{ left: imglist + 'px' }">
              <li
                v-for="(img, index) in imagessrc"
                @click="imgClick($event)"
                :key="index"
              >
                <img :src="img.s" alt="list" :data-key="index" />
              </li>
            </ul>
          </div>
          <a href="javascript:;" @click="next">＞</a>
        </div>
      </div>
      <div class="content-right">
        <div class="right-top">
          <div class="title">
            <h3>{{ goodsDetail.title }}</h3>
            <p>{{ goodsDetail.recommend }}</p>
          </div>
          <div class="price">
            <div class="price-top">
              <div class="left">
                <span>價&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;格</span>
              </div>
              <div class="right">
                <div>
                  <p>￥</p>
                  <p>{{ totalPrice }}</p>
                  <i>降價通知</i>
                </div>
                <span>累計評價&nbsp;{{ goodsDetail.evaluateNum }}</span>
              </div>
            </div>
            <div class="price-bottom">
              <div class="left">
                <span>促&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;銷</span>
              </div>
              <div class="right">
                <span> {{ goodsDetail.type }}</span>
                <span> {{ goodsDetail.content }}</span>
              </div>
            </div>
          </div>
          <div class="support">
            <span>支&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;持</span>
            <p>{{ goodsDetail.support }}</p>
          </div>
          <div class="address">
            <span>配&nbsp;送&nbsp;至</span>
            <p>{{ goodsDetail.address }}</p>
          </div>
        </div>
        <div class="right-bottom">
          <div class="detail">
            <div class="item-detail" v-if="choose.color.title">
              {{ choose.color.title
              }}<a href="javascript:;" @click="delItem(0, choose.color.price)"
                >X</a
              >
            </div>
            <div class="item-detail" v-if="choose.GB.title">
              {{ choose.GB.title
              }}<a href="javascript:;" @click="delItem(1, choose.GB.price)"
                >X</a
              >
            </div>
            <div class="item-detail" v-if="choose.version.title">
              {{ choose.version.title
              }}<a href="javascript:;" @click="delItem(2, choose.version.price)"
                >X</a
              >
            </div>
            <div class="item-detail" v-if="choose.buy.title">
              {{ choose.buy.title
              }}<a href="javascript:;" @click="delItem(3, choose.buy.price)"
                >X</a
              >
            </div>
          </div>
          <div class="select">
            <dl
              ref="detailData"
              v-for="(datail, type) in goodsDetail.crumbData"
              :key="type"
            >
              <dt>{{ datail.title }}</dt>
              <dd
                v-for="(data, index) in datail.data"
                :key="index"
                :data-key="index"
                :data-type="type"
                @click="chooseDatail($event)"
              >
                {{ data.type }}
              </dd>
            </dl>
          </div>
          <div class="shopping">
            <div class="add">
              <input type="text" v-model="count" />
              <a href="javascript:;" @click="count++">+</a>
              <a href="javascript:;" @click="count === 1 ? 1 : count--">-</a>
            </div>
            <button>加入購物車</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "MainPage",
  data() {
    return {
      mask_top: 0,
      mask_left: 0,
      smallImgSrc: "./images/s1.png",
      bigImgSrc: "./images/b1.png",
      show: false,
      goodsDetail: {},
      imagessrc: [],
      path: [],
      imglist: 0,
      choose: {
        color: {
          title: "",
          price: 0,
        },
        GB: {
          title: "",
          price: 0,
        },
        version: {
          title: "",
          price: 0,
        },
        buy: {
          title: "",
          price: 0,
        },
      },
      count: 1,
    };
  },
  beforeMount() {
    let url = "data.json"
    axios
      .get(url)
      .then((result) => {
        const { goodsDetail, imagessrc, path } = result.data;
        this.goodsDetail = goodsDetail;
        this.imagessrc = imagessrc;
        this.path = path;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  mounted() {
    this.$bus.$emit("price", 5299);
  },
  computed: {
    totalPrice() {
      this.$bus.$emit(
        "price",
        (this.goodsDetail.price +
          this.choose.color.price +
          this.choose.GB.price +
          this.choose.version.price +
          this.choose.buy.price) *
          this.count
      );
      return (
        (this.goodsDetail.price +
          this.choose.color.price +
          this.choose.GB.price +
          this.choose.version.price +
          this.choose.buy.price) *
        this.count
      );
    },
  },
  methods: {
    MouseMove(e) {
      this.mask_top =
        e.clientY -
        this.$refs.smallImg.getBoundingClientRect().top -
        this.$refs.smallImg.offsetHeight / 4;
      this.mask_left =
        e.clientX -
        this.$refs.smallImg.getBoundingClientRect().left -
        this.$refs.smallImg.offsetWidth / 4;
      if (this.mask_top <= 0) {
        this.mask_top = 0;
      } else if (this.mask_top >= 198) {
        this.mask_top = 198;
      }
      if (this.mask_left <= 0) {
        this.mask_left = 0;
      } else if (this.mask_left >= 198) {
        this.mask_left = 198;
      }
    },
    imgClick(e) {
      let src = e.target.dataset.key;
      this.bigImgSrc = this.imagessrc[src].b;
      this.smallImgSrc = this.imagessrc[src].s;
    },
    prev() {
      if (this.imglist == 0) return;
      this.imglist += 152;
    },
    next() {
      if (this.imglist == -608) return;
      this.imglist -= 152;
    },
    chooseDatail(event) {
      let type = event.target.dataset.type;
      let select = event.target.dataset.key;
      for (let j = 0; j < this.$refs.detailData[type].childNodes.length; j++) {
        this.$refs.detailData[type].childNodes[j].style.color = "#666";
      }
      this.$refs.detailData[type].childNodes[select * 1 + 1].style.color =
        "red";

      if (type == 0) {
        this.choose.color.price =
          this.goodsDetail.crumbData[type].data[select].changePrice;
        this.choose.color.title =
          this.$refs.detailData[type].childNodes[select * 1 + 1].innerText;
      } else if (type == 1) {
        this.choose.GB.price =
          this.goodsDetail.crumbData[type].data[select].changePrice;
        this.choose.GB.title =
          this.$refs.detailData[type].childNodes[select * 1 + 1].innerText;
      } else if (type == 2) {
        this.choose.version.price =
          this.goodsDetail.crumbData[type].data[select].changePrice;
        this.choose.version.title =
          this.$refs.detailData[type].childNodes[select * 1 + 1].innerText;
      } else if (type == 3) {
        this.choose.buy.price =
          this.goodsDetail.crumbData[type].data[select].changePrice;
        this.choose.buy.title =
          this.$refs.detailData[type].childNodes[select * 1 + 1].innerText;
      }
      this.$bus.$emit("price", this.totalPrice);
    },
    delItem(item) {
      if (item == 0) {
        this.choose.color.title = "";
        this.choose.color.price = 0;
      } else if (item == 1) {
        this.choose.GB.title = "";
        this.choose.GB.price = 0;
      } else if (item == 2) {
        this.choose.version.title = "";
        this.choose.version.price = 0;
      } else if (item == 3) {
        this.choose.buy.title = "";
        this.choose.buy.price = 0;
      }
      for (let j = 0; j < this.$refs.detailData[item].childNodes.length; j++) {
        this.$refs.detailData[item].childNodes[j].style.color = "#666";
      }
      this.$refs.detailData[item].childNodes[1].style.color = "red";
      this.$bus.$emit("price", this.totalPrice);
    },
  },
};
</script>

<style lang="sass" scoped>
.container
  width: 1200px
  margin: 15px auto 0 auto
  .nav
    display: flex
    align-items: center
    padding: 9px 15px 9px 0
    font-size: 0px
    a
      font-size: 12px
    i
      padding: 0 5px
      font-size: 12px
  .content
    margin: 5px 0px 15px
    display: flex
    position: relative
    justify-content: space-between
    .content-left
      .left-top
        display: flex
        .small-img
          position: relative
          width: 400px
          height: 400px
          >img
            box-sizing: border-box
            width: 400px
            height: 400px
            border: 1px solid #DFDFDF
          .mask
            width: 200px
            height: 200px
            background-color: rgba(255, 255, 255, .5)
            border: 1px solid #ddd
            position: absolute
            pointer-events: none
        .big-img
          position: absolute
          left: 400px
          .big
            box-sizing: border-box
            margin-left: 20px
            width: 400px
            height: 400px
            border: 1px solid #ddd
            overflow: hidden
            position: relative
            z-index: 1
            >img
              position: absolute
              width: 800px
              height: 800px
      .left-bottom
        width: 400px
        margin-top: 5px
        display: flex
        justify-content: space-between
        >a
          width: 10px
          height: 54px
          border: 1px solid #ccc
          background-color: #EBEBEB
          line-height: 54px
          text-align: center
          &:first-child
            margin-right: 4px
        .imglist
          position: relative
          width: 372px
          height: 56px
          overflow: hidden
          >ul
            position: absolute
            display: flex
            transition: .5s
            left: 0
            >li
              >img
                width: 50px
                height: 50px
                border: 1px solid #ccc
                padding: 2px
                margin-right: 20px
    .content-right
      width: 700px
      .right-top
        .title
          >h3
            font-size: 14px
            line-height: 21px
            margin-top: 15px
          >p
            color: #e12228
            margin-top: 15px
        .price
          margin-top: 10px
          line-height: 28px
          background-color: #fee9ec
          padding: 7px
          .price-top
            display: flex
            .left
              margin-right: 15px
              >span
            .right
              width: 100%
              display: flex
              justify-content: space-between
              >div
                display: flex
                >p
                  font-size: 24px
                  font-weight: bold
                  color: #cc1122
                  &:first-child
                    font-size: 16px
                >i
                  font-size: 12px
                  color: #cc1122
              >span
                padding: auto 0
          .price-bottom
            line-height: 28px
            display: flex
            .left
              margin-right: 15px
              >span
            .right
              width: 520px
              >span
                color: #999
                &:first-child
                  background-color: #c81623
                  padding: 3px
                  color: #fff
        .support
          display: flex
          margin-top: 10px
          line-height: 28px
          >span
            margin-right: 15px
          >p
            width: 520px
            color: #999
        .address
          display: flex
          border-bottom: 1px solid #ededed
          padding-bottom: 5px
          margin-top: 10px
          line-height: 28px
          >span
            margin-right: 15px
          >p
            width: 520px
            color: #999
      .right-bottom
        line-height: 28px
        .detail
          display: flex
          .item-detail
            margin-top: 10px
            height: 30px
            background-color: snow
            border: 1px solid #ddd
            padding: 0px 20px
            margin-right: 20px
            line-height: 30px
            text-align: center
            >a
              color: red
              margin-left: 20px
        .select
          >dl
            display: flex
            margin: 13px 0
            >dt
              margin-right: 15px
            >dd
              margin-right: 5px
              color: #666
              line-height: 24px
              padding: 2px 14px
              border-top: 1px solid #eee
              border-left: 1px solid #eee
              border-right: 1px solid #bbb
              border-bottom: 1px solid #bbb
              &:first-of-type
                color: red
        .shopping
          display: flex
          .add
            width: 55px
            margin-right: 15px
            position: relative
            input
              width: 38px
              height: 37px
              border: 1px solid #ddd
              color: #555
              text-align: center
              font-size: 18px
            >a
              position: absolute
              width: 15px
              height: 18px
              line-height: 18px
              background-color: #f1f1f1
              color: #666
              text-align: center
              right: 1px
              border: 1px solid #ddd
              &:last-child
                border-top: 0
                top: 20px
          >button
            padding: 0 25px
            height: 36px
            font-size: 16px
            background-color: #e1251b
            color: #fff
            border: none
</style>
