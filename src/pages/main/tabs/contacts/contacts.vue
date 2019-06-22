<template>
  <f7-page class="film-view" v-if="tabShow">
    <!-- <f7-searchbar
      search-container="#search-list"
      :disable-link-text="$t('app.cancel')"
      :placeholder="$t('contacts.placeholder')"
      :clear-button="true"
    ></f7-searchbar>-->

    <!-- <f7-list contacts-list id="search-list" class="searchbar-found">
      <f7-list-group v-for="(group, key) in contactGroups" :key="key">
        <f7-list-item :title="key" group-title></f7-list-item>
        <f7-list-item v-for="contact in group"
          :link="getLink(contact.nickname)"
          :key="contact.nickname"
          :title="contact.nickname"
          :after="contact.location"
          :media="getAvatarMedia(contact.avatar)"
        ></f7-list-item>
      </f7-list-group>
    </f7-list>
    <f7-list class="searchbar-not-found">
      <div class="empty-content">
        <i class="iconfont icon-wujieguoyangshi"></i>
        <div class="text">{{$t('contacts.empty')}}</div>
      </div>
    </f7-list>-->

    <div class="film-video">
      <p class="film-back"></p>
    </div>
    <div class="film-info">
      <div class="film-info-part-1">
        <p class="film-rate">9.3</p>
      </div>
      <div class="film-info-part-2">
        <div class="film-name">
          <p>蜘蛛侠：平行空间</p>
        </div>
        <div class="film-info-detail">
          <!-- <p>9.3分</p> -->
          <p class="film-info-category">动画 / 科幻 / 情感</p>
          <p class="film-info-category">美国</p>
        </div>
        <div class="film-info-detail-bottom">
          <p>45.6万热度</p>
          <p>124分钟</p>
          <p>35981已看</p>
        </div>
      </div>
    </div>
    <div class="film-intro">
      <p>简介</p>
      <p>令人叹为观止的想像力在《蜘蛛侠：平行空间》里成功的将分属得很好很好，cv很好令人叹为观止的想像力在《蜘蛛侠：平行空间》里成功的将分属得…</p>
    </div>
    <!-- <div class="film-opera">
      <div class="film-saying">

      </div>
      <div class="film-share">

      </div>
    </div>-->

    <div class="film-tabs">
      <van-tabs v-model="activeTab" :line-width="32">
        <van-tab title="角色表"></van-tab>
        <van-tab title="剧照"></van-tab>
        <van-tab title="预告片"></van-tab>
      </van-tabs>
      <div class="film-tab-content">
        <div class="film-tab-1 film-players">
          <p></p>
          <p></p>
          <p></p>
        </div>
        <div class="film-tab-2 film-photos"></div>
        <div class="film-tab-3 film-videos"></div>
      </div>

      <div class="film-photo">
        <div class="film-photo-part-1">
          <div></div>
        </div>
        <div class="film-photo-part-2">
          <div class="film-photo-middle"></div>
          <div class="film-photo-small">
            <div></div>
            <div>
              <p>MORE</p>
            </div>
          </div>
        </div>
      </div>
      <div class="film-review"></div>
    </div>

    <!-- popup -->
    <div class="film-comments">
      <div class="long-comments"></div>
      <div class="short-comments"></div>
    </div>
  </f7-page>
</template>

<style lang="less">
.film-tabs .van-hairline--top-bottom::after {
  border-width: 0;
}
</style>

<style lang="less" scoped>
@color-1: #7d7e80;
@font-size-1: 14px;

p {
  margin: 0;
}

.film-view {
}

.film-photo {
  display: flex;
  justify-content: space-between;
  padding: 15px;
}

.film-photo-part-1 {
  width: 60%;
  height: 8.5rem;
  background-color: rgb(242, 242, 242);
  border-radius: 6px;
  margin-right: 5px;
  flex: 1;
}

.film-photo-part-2 {
  width: 40%;
  display: flex;
  flex-direction: column;
}

.film-photo-part-2 .film-photo-middle {
  height: 45%;
  background-color: rgb(244, 244, 244);
  margin-bottom: 5px;
  border-radius: 6px;
  flex: 1;
}

.film-photo-part-2 .film-photo-small {
  height: 45%;
  flex: 1;
  display: flex;
  justify-content: space-between;
}

.film-photo-part-2 .film-photo-small div{
  flex: 1;
  border-radius: 6px;
}

.film-photo-part-2 .film-photo-small div:first-child{
  margin-right: 5px;
  background-color: rgb(245, 245, 245);
}

.film-photo-part-2 .film-photo-small div:last-child{
  position: relative;
  background-color: rgb(247, 247, 247);
}

.film-photo-part-2 .film-photo-small div:last-child p{
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 100%;
  text-align: center;
  color: @color-1;
}

.film-video {
  height: 200px;
  background-color: #eee;
  margin-bottom: 15px;
  position: relative;
}

.film-back {
  position: absolute;
  top: 20px;
  left: 20px;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  background-color: rgba(0, 0, 0, 0.3);
}

.film-info {
  display: flex;
  padding: 0 15px;
}

.film-info-part-1 {
  width: 80px;
  height: 100px;
  background-color: #eee;
  border-radius: 6px;
  overflow: hidden;
  position: relative;
}

.film-rate {
  padding: 0 6px;
  border-top-left-radius: 6px;
  position: absolute;
  right: 0;
  bottom: 0;
  // width: 100%;
  text-align: center;
  background-color: rgba(0, 0, 0, 0.2);
  font-size: 12px;
}

.film-info-part-2 {
  flex: 1;
  position: relative;
  padding-left: 10px;
}

.film-name {
  font-size: 1.125rem;
  margin: 3px 0;
}

.film-info-detail {
  height: auto;
}

.film-info-category {
  font-size: 13px;
}

.film-info-detail-bottom {
  position: absolute;
  bottom: 0;
  color: @color-1;
  display: flex;
  width: 95%;
}

.film-info-detail-bottom p {
  margin-right: 15px;
  font-size: 13px;
}

.film-info-detail p {
  // margin: 0;
  color: @color-1;
}

.film-intro {
  margin-top: 15px;
  padding: 0 20px;
}

.film-intro p:first-child {
  font-size: 14px;
  margin: 3px 0;
}

.film-intro p:last-child {
  color: @color-1;
  text-align: justify;
  font-size: 13px;
}

.film-tabs {
  margin-top: 10px;
}
</style>


<script>
import groupBy from "lodash/groupBy";
import { mapState } from "vuex";
import { getRemoteAvatar } from "@/utils/appFunc";

import { Tab, Tabs } from "vant";

export default {
  data() {
    return {
      tabShow: false,
      activeTab: 0
    };
  },
  mounted() {
    let _this = this;
    this.$EventBus.$on("indexTabsChange", res => {
      if (res == "contacts") {
        console.log("tab2 已经渲染");
        this.tabShow = true;
      } else {
        this.tabShow = false;
      }
    });
  }
};
</script>
