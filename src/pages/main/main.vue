<template>
  <f7-page>
    <!-- <f7-navbar>
      <f7-nav-left></f7-nav-left>
      <f7-nav-title>{{navbarTitle}}</f7-nav-title>
      <f7-nav-right>
        <f7-link icon="iconfont icon-feedback3" icon-size="22" v-show="activedTab === 'home'" @click="openPublisher"></f7-link>
      </f7-nav-right>
    </f7-navbar>-->
    <!-- <f7-toolbar tabbar :labels="!isAndroid">
      <f7-link :icon="!isAndroid ? 'iconfont icon-ios7homeoutline' : ''" :text="$t('app.home')" tab-link="#home" tab-link-active></f7-link>
      <f7-link :icon="!isAndroid ? 'iconfont icon-ios7chatbubbleoutline' : ''" :text="$t('app.contacts')" tab-link="#contacts"></f7-link>
      <f7-link :icon="!isAndroid ? 'iconfont icon-ios7gearoutline' : ''" :text="$t('app.settings')" tab-link="#settings"></f7-link>
    </f7-toolbar>-->

    <div class="toolbar">
      <div class="toolbar-inner">
        <a href="#home" class="tab-link tab-link-active">
          <i class="f7-icons">icon videocam</i>
          <span class="tabbar-label">首页</span>
        </a>
        <a href="#contacts" class="tab-link">
          <i class="f7-icons">icon play</i>
          <span class="tabbar-label">创意</span>
        </a>
        <a href="#settings" class="tab-link">
          <i class="f7-icons">icon cloud</i>
          <span class="tabbar-label">个人</span>
        </a>
      </div>
    </div>

    <f7-tabs>
      <f7-tab id="home" tab-active @tab:show="tabActived('home')">
        <home-view @show-tip="showLoadResult"></home-view>
      </f7-tab>
      <f7-tab id="contacts" @tab:show="tabActived('contacts')">
        <contacts-view></contacts-view>
      </f7-tab>
      <f7-tab id="settings" @tab:show="tabActived('settings')">
        <settings-view></settings-view>
      </f7-tab>
    </f7-tabs>

    <div class="load-result">{{$t('home.noNewestPost')}}</div>
  </f7-page>
</template>

<style>
.auto-navbar .searchbar-disable-button {
  color: #9e9ea2 !important;
}

.ios .searchbar input[type="text"],
.ios .searchbar input[type="search"] {
  background-color: #f6f6f6 !important;
}

.toolbar {
  background: #fefefe !important;
}

.category a{
  color: #000;
}

.ios .toolbar:before {
  background-color: #fff !important;
}

.ios .tab-link{
  color: #7b7e80;
}

.ios .tab-link-active{
  color: #000;
}

.ios .searchbar-disable-button{
  font-size: 15px;
}

.auto-navbar {
  background-color: #fff !important;
}
</style>

<style lang="less" scoped>
.load-result {
  width: 100%;
  height: 30px;
  position: absolute;
  bottom: 50px;
  left: 0;
  background-color: #ff9500;
  color: #ffffff;
  z-index: 5001;
  text-align: center;
  line-height: 30px;
  opacity: 0;
}
.md {
  .load-result {
    bottom: 0;
  }
}

.toolbar {
  position: fixed !important;
  bottom: 0; 
}

.toolbar:before {
  background-color: #fff !important;
}

.toolbar-inner {
  display: flex;
  justify-content: space-between;
  padding: 0 55px;
}

.tab-link{
  display: flex;
  flex-direction: column;
  justify-content: center;
  line-height: 30px;
}

.tab-link .f7-icons{
  font-size: 14.5px;
  line-height: 17px;
}

.tab-link .tabbar-labels{
  /* height: 50px !important; */
}

.tab-link .tabbar-label{
  font-size: 12px !important;
  line-height: 18px;
}

.tabbar a.tab-link {
  width: 100% !important;
  min-width: auto !important;
}

.tabbar-labels span.tabbar-label {
  /* font-size: 11px !important; */
}

.size-20 {
  font-size: 20px;
}

.color-custom-2 {
  color: #fff;
}

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

.navbar:after {
  background-color: #fff !important;
}

.search-bar {
  padding: 10px 10px 5px 10px;
  display: flex;
  align-items: center;
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
</style>


<script>
import HomeView from "./tabs/home";
import ContactsView from "./tabs/contacts";
import SettingsView from "./tabs/settings";
import { mapActions } from "vuex";
import { isAndroid } from "@/utils/appFunc";
require("../../assets/styles/framework7-icons/css/framework7-icons.css");

export default {
  data() {
    return {
      activedTab: "home"
    };
  },
  computed: {
    // navbarTitle() {
    //   switch (this.activedTab) {
    //     case "home":
    //       return this.$t("app.app_name");
    //     case "contacts":
    //       return this.$t("app.contacts");
    //     case "settings":
    //       return this.$t("app.settings");
    //   }
    // },
    isAndroid() {
      return isAndroid();
    }
  },
  mounted(){
    this.$EventBus.$emit("indexTabsChange", this.activedTab)
  },
  methods: {
    ...mapActions(["updatePopup"]),
    tabActived(tab) {
      // this.activedTab = tab;
      this.$EventBus.$emit("indexTabsChange", tab)
    },
    showLoadResult() {
      setTimeout(_ => {
        this.$$("div.load-result")
          .css("opacity", "1")
          .transition(1000);

        setTimeout(_ => {
          this.$$("div.load-result")
            .css("opacity", "0")
            .transition(1000);
        }, 2100);
      }, 400);
    },
    openPublisher() {
      this.updatePopup({
        key: "publisherOpened",
        value: true
      });
    }
  },
  components: {
    HomeView,
    ContactsView,
    SettingsView
  }
};
</script>
