<template>
  <div id="home">
    <div id="banner">
      <home-banner/>
    </div>
    <div id="live-banner" class="common-banner">
      <live-banner/>
    </div>
    <div id="recommend-banner" class="common-banner">
      <recommend/>
    </div>
    <div id="advertising" class="common-banner">
      <advertising/>
    </div>
    <div id="ranking" class="common-banner">
      <ranking/>
    </div>
  </div>
</template>

<script>
import HomeBanner from "@/components/content/main/home/banner/HomeBanner";
import LiveBanner from "@/components/content/main/home/live/LiveBanner";
import Recommend from "@/components/content/main/home/recommend/Recommend";
import Advertising from "@/components/content/main/home/advertising/Advertising";
import Ranking from "@/components/content/main/home/ranking/Ranking";

export default {
  name: "Home",
  components: {
    Ranking,
    Advertising,
    Recommend,
    LiveBanner,
    HomeBanner
  }
}
</script>

<style scoped>
#home {
  padding: 0;
  margin: 0 auto;
  width: 1200px;
  height: 100%;
}

#banner {
  margin: 0 0 40px 0;
  width: 1200px;
}

.common-banner {
  width: 1200px;
  padding-bottom: 40px;
  flex-wrap: wrap;
}
</style>
