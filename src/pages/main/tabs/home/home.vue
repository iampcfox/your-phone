<template>
  <div>
    <!-- <div class="navbar search-bar">
      <i class="f7-icons size-24 color-custom-1">sort</i>
      <form
        data-search-list=".search-here"
        data-search-in=".item-title"
        class="searchbar searchbar-init"
      >
        <div class="searchbar-input">
          <input type="search" placeholder="Sweetheart - 邓福如">
          <a href="#" class="searchbar-clear"></a>
        </div>
        <a href="#" class="searchbar-cancel">取消</a>
      </form>
    </div>-->


    <f7-navbar title="Searchbar" class="auto-navbar">
      <i class="f7-icons size-24 color-custom-1">sort</i>
      <f7-searchbar
        search-container=".search-list"
        search-in=".item-title"
        disable-button-text="取消"
      ></f7-searchbar>
    </f7-navbar>

    <f7-page
      id="homeView"
      class="home-view"
      ptr
      infinite
      @ptr:refresh="onRefresh"
      @infinite="onInfiniteScroll"
    >
      <div class="media-list">
        <div
          data-pagination=".swiper-pagination-c3"
          data-space-between="30"
          data-slides-per-view="1"
          class="swiper-container swiper-init ks-carousel-slider"
        >
          <div class="swiper-pagination swiper-pagination-c3"></div>
          <div class="swiper-wrapper">
            <div class="swiper-slide">Slide 1</div>
            <div class="swiper-slide">Slide 2</div>
            <div class="swiper-slide">Slide 3</div>
          </div>
        </div>

        <div class="category">
          <ul>
            <li>
              <p>
                <i class="f7-icons size-20 color-custom-2">fire</i>
              </p>
              <p>
                <a href="/collectionmusic/">正在热映</a>
              </p>
            </li>
            <li>
              <p>
                <i class="f7-icons size-20 color-custom-2">paper_plane</i>
              </p>
              <p>即将上映</p>
            </li>
            <li>
              <p>
                <i class="f7-icons size-20 color-custom-2">bars_chart</i>
              </p>
              <p>Top250</p>
            </li>
            <li>
              <p>
                <i class="f7-icons size-20 color-custom-2">infinite</i>
              </p>
              <p>口碑榜</p>
            </li>
            <li>
              <p>
                <i class="f7-icons size-20 color-custom-2">layers</i>
              </p>
              <p>新片榜</p>
            </li>
          </ul>
        </div>

        <div class="recommend">
          <div class="r-header">
            <p>推荐电影</p>
            <p>更多</p>
          </div>

          <div class="r-list">
            <div class="r-item">
              <p></p>
              <p>读书，然后忘记背景音乐（12-4更新）</p>
            </div>
            <div class="r-item">
              <p></p>
              <p>读书，然后忘记背景音乐（12-4更新）</p>
            </div>
            <div class="r-item">
              <p></p>
              <p>读书，然后忘记背景音乐（12-4更新）</p>
            </div>
            <div class="r-item">
              <p></p>
              <p>读书，然后忘记背景音乐（12-4更新）</p>
            </div>
            <div class="r-item">
              <p></p>
              <p>读书，然后忘记背景音乐（12-4更新）</p>
            </div>
            <div class="r-item">
              <p></p>
              <p>读书，然后忘记背景音乐（12-4更新）</p>
            </div>
          </div>
        </div>
      </div>
    </f7-page>
  </div>
</template>

<script>
import axios from "axios";
import Card from "@/components/card";
import { mapState, mapActions } from "vuex";

export default {
  data() {
    return {
      tabShow: false,
      refreshing: false,
      loadingMore: false,
      loadedEnd: false
    };
  },
  computed: {
    ...mapState({
      timeline: state => state.timeline
    })
  },
  mounted() {
    // this.getTimeline();

    this.$EventBus.$on("indexTabsChange", res => {
      if (res == "home") {
        console.log("tab1 已经渲染");
        this.tabShow = true;
      }else{
        this.tabShow = false;
      }
    });
  },
  methods: {
    ...mapActions(["initTimeline", "infiniteTimeline", "refreshTimeline"]),
    getTimeline() {
      this.$f7.preloader.show();
      let _this = this;
      setTimeout(() => {
        axios.get("/timeline.json").then(res => {
          const timeline = res.data;
          _this.initTimeline(timeline);
          _this.$f7.preloader.hide();
        });
      }, 3000);
    },
    onRefresh() {
      // if (this.refreshing) return false;

      // this.refreshing = true;
      // axios.get("/refresh_timeline.json").then(res => {
      //   if (parseInt(this.timeline[0].id) === 48) {
      //     this.$emit("show-tip");
      //   } else {
      //     const timeline = res.data;
      //     this.refreshTimeline(timeline);
      //   }
      //   this.refreshing = false;
      //   this.$f7.ptr.done();
      // });

      setTimeout(() => {
        this.refreshing = false;
        this.$f7.ptr.done();
      }, 1000);
    },
    onInfiniteScroll() {
      // if (this.loadingMore || this.loadedEnd) return false;

      // this.loadingMore = true;
      // axios.get("/more_timeline.json").then(res => {
      //   const id = parseInt(this.timeline[this.timeline.length - 1].id);
      //   if (id === 24) {
      //     this.loadedEnd = true;
      //     this.$f7.infiniteScroll.destroy("#homeView .infinite-scroll-content");
      //     this.$$("#homeView .infinite-scroll-preloader").remove();
      //   } else {
      //     const timeline = res.data;
      //     this.infiniteTimeline(timeline);
      //   }
      //   this.loadingMore = false;
      // });
    },
    routeToPost(data) {
      this.$f7router.navigate(`/post/?mid=${data.id}`);
    }
  },
  components: {
    Card
  }
};
</script>

<style>

</style>

<style scoped>
.size-24 {
  font-size: 20px;
}

.color-custom-1 {
  color: #cecece;
}

.size-20 {
  font-size: 20px;
}

.color-custom-2 {
  color: #fff;
}

.navbar{
  position: fixed;
}

.navbar:after {
  background-color: #fff !important;
}

.search-bar {
  padding: 10px 10px 5px 10px;
  display: flex;
  align-items: center;
  position: fixed;
}

.searchbar-cancel {
  font-size: 15px !important;
}

.search-bar,
.pages,
.page-content {
  background-color: #fff;
}

.page {
  background: #fff !important;
}

.searchbar {
  padding-right: 12px !important;
  height: 34px;
  background-color: #fff;
}

.searchbar:after {
  background-color: #fff;
}

.searchbar input {
  background-color: #f6f6f6 !important;
}

.search-bar,
.pages,
.page-content {
  background-color: #fff;
}

.page {
  background: #fff !important;
}

.swiper-container {
  padding-top: 10px;
  height: 110px;
}

.swiper-wrapper {
  margin: 0 10px;
}

.swiper-slide {
  z-index: 999999;
  width: calc(100% - 10px * 2) !important;
  border-radius: 8px;
  border: none !important;
  background-color: #f6f6f6 !important;
}

.swiper-slide:nth-child(2) {
  transform: translateX(20px);
}

.swiper-slide:nth-child(3) {
  transform: translateX(40px);
}

.no-navbar {
  padding-top: 0 !important;
}

.category {
  border-bottom: 1px solid #f6f6f6;
  padding-bottom: 10px;
}

.category ul {
  padding: 0 5px;
  display: flex;
  justify-content: space-between;
  font-size: 10px;
}

.category ul li {
  list-style: none;
  width: calc(100% / 5);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.category ul li p {
  text-align: center;
  margin-bottom: 0;
}

.category ul li p:first-child {
  width: 24px;
  height: 24px;
  background-color: #ff372b;
  border-radius: 50%;
  padding: 3px;
  line-height: 24px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.r-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px 10px 10px;
}

.r-header p {
  margin-bottom: 0;
}

.r-header p:first-child {
  font-size: 15px;
}

.r-header p:last-child {
  font-size: 12px;
  padding: 2px 8px;
  border: 1px solid #cecece;
  border-radius: 12px;
  text-align: center;
}

.r-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 0 10px;
}

.r-list p {
  margin: 0;
}

.r-item {
  width: 31%;
  margin-bottom: 10px;
}

.r-item p:first-child {
  border-radius: 6px;
  width: 100%;
  padding-top: 100%;
  background-color: #eee;
}

.r-item p:last-child {
  font-size: 11px;
  margin-top: 5px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
</style>