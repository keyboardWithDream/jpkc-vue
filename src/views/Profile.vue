<template>
  <div id="profile">
    <el-container style="height: 100%">
      <el-aside style="width: 200px; border-radius: 8px">
        <nav-menu @menuSelect="menuSelect"/>
      </el-aside>
      <el-main>
        <router-view name="profileContent"/>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import NavMenu from "@/components/content/main/profile/NavMenu";
export default {
  name: "Profile",
  components: {NavMenu},
  data() {
    return {
      activeMenu: '1'
    }
  },
  methods: {
    menuSelect(key, keyPath) {
      this.$router.push('/profile/' + key)
    }
  }
}
</script>

<style scoped>
#profile {
  margin: 0 auto;
  width: 1200px;
}

.el-main {
  background-color: #fff;
  border-radius: 8px;
  margin-left: 10px;
  margin-top: 0;
}

.el-aside {
  border-radius: 8px;
  height: 100%;
}
</style>
