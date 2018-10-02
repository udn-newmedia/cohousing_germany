<template>
  <div class="wrapper">
    <div class="banner-wrapper" :style="{width: width, transform: distance}">
      <div class="you-know-group" :style="{width: width_article}">
        <div class="you-know-line"></div>
        <div class="you-know">你或許想知道更多</div>
        <div class="you-know-line"></div>
      </div>
      <div class="banner-group">
        <div class="banner">
          <a @click="handle_GA_1" target="_blank" :href="href_1">
            <div class="circle-wrapper">
              <img class="img-wrapper" :src="src_1" alt="">
            </div>
          </a>
          <a @click="handle_GA_1" target="_blank" :href="href_1">願景工程「世代共融」系列報導</a>
        </div>
        <div class="banner">
          <a @click="handle_GA_2" target="_blank" :href="href_2">
            <div class="circle-wrapper">
              <img class="img-wrapper" :src="src_2" alt="">
            </div>
          </a>
          <a @click="handle_GA_2" target="_blank" :href="href_2">如何用社會創新，促進世代共融？</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import _debounce from "lodash.debounce"
export default {
  name: "Banner",
  props: {
    src_1: {
      type: String
    },
    src_2: {
      type: String
    },
    href_1: {
      type: String
    },
    href_2: {
      type: String
    }
  },
  data() {
    return {
      distance: "",
      width: "",
      width_article: "",
      windowWidth: global.innerWidth
    };
  },
  methods: {
    handle_GA_1: function () {
      const self = this
      ga("send", {
          "hitType": "event",
          "eventCategory": "超連結",
          "eventAction": "click",
          "eventLabel": "[" + Utils.detectPlatform() + "] [" + document.querySelector('title').innerHTML + "] [BannerLink: " + self.href_1 + "]"
        });
    },
    handle_GA_2: function () {
      const self = this
      ga("send", {
          "hitType": "event",
          "eventCategory": "超連結",
          "eventAction": "click",
          "eventLabel": "[" + Utils.detectPlatform() + "] [" + document.querySelector('title').innerHTML + "] [BannerLink: " + self.href_2 + "]"
        });
  	}
  },
  created() {
    $(window).on(
      "resize",
      _debounce(() => {
        if (this.windowWidth !== global.innerWidth) {
          this.windowWidth = global.innerWidth
          this.width = $(".article_container")[0].clientWidth + "px";
          this.width_article = $(".article")[0].clientWidth + "px";
          this.distance = "translateX(" + ($(".article_container")[0].clientWidth - $(".article")[0].clientWidth) * -0.5 + "px)";
          this.$forceUpdate()
        }
      }, 200)
    )
  },
  mounted() {
    this.width = $(".article_container")[0].clientWidth + "px";
    this.width_article = $(".article")[0].clientWidth + "px";
    this.distance = "translateX(" + ($(".article_container")[0].clientWidth - $(".article")[0].clientWidth) * -0.5 + "px)";
  },
};
</script>

<style scoped>
  a {
    font-size: 22px;
    font-weight: bold;
    text-decoration:underline;
    color: #ffffff;
  }
  .banner-wrapper {
    padding: 100px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: #9dd1d5;
  }
  .you-know-group {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .you-know-line {
    margin: 10px;
    width: 75px;
    height: 1px;
    background: #ffffff;
  }
  .you-know {
    font-size: 18px;
    font-weight: bold;
    color: #ffffff;
  }
  .banner-group {
    margin-top: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .banner {
    margin-left: 80px;
    margin-right: 80px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .circle-wrapper {
    width: 265px;
    height: 265px;
    border-radius: 50%;
    margin-bottom: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #ffffff;
  }
  .img-wrapper {
    width: 250px;
    height: 250px;
    border-radius: 50%;
    transition: transform 333ms ease-in-out
  }

  .img-wrapper:hover {
    transform: scale(1.08);
  }

  @media screen and (max-width: 767px) {
    .banner-wrapper {
      padding: 50px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background-color: #9dd1d5;
    }
    .banner-group {
      flex-direction: column;
    }
    .banner {
      margin-left: 0;
      margin-right: 0;
      margin-top: 50px;
      margin-bottom: 50px;
    }
  }
</style>
