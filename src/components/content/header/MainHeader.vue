<template>
  <div id="main-header">
    <login-dialog/>
    <el-row :gutter="0">
      <el-col :span="4">
        <img @click="$router.push('/home')" src="~assets/images/logo.png" alt="logo">
      </el-col>
      <el-col :span="8" :offset="1">
        <div class="content">
          <drop-down id="drop-down" :title="dropdownTitle" @clickCategory="clickCategory" :items="dropdownItems"/>
          <el-button type="text" @click="linkToSchoolView">学校</el-button>
          <el-button type="text" @click="linkToCourse">所有课程</el-button>
          <el-button type="text" @click="linkToLCourse">课程直播</el-button>
          <el-button type="text" @click="linkToTeacher">名师辅导</el-button>
        </div>
      </el-col>
      <el-col :span="6" :offset="2">
        <search-input id="search-input" placeholder="请输入感兴趣的课程"/>
      </el-col>
      <el-col :span="2" :offset="1">
        <el-button v-if="$store.state.token === null" @click="activeLoginDialog" type="text">注册<el-divider direction="vertical"/>登录</el-button>
        <div v-else>
          <el-dropdown>
            <el-button @click="linkToProfile" type="text">个人中心</el-button>
            <template #dropdown>
              <el-dropdown-menu>
                <el-dropdown-item @click.native="changeAccount">切换账号</el-dropdown-item>
                <el-dropdown-item @click.native="logout">退出登录</el-dropdown-item>
              </el-dropdown-menu>
            </template>
          </el-dropdown>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import DropDown from "@/components/common/DropDown";
import SearchInput from "@/components/common/SearchInput";
import LoginDialog from "@/components/content/dialog/login/LoginDialog";
import Avatar from "@/components/common/Avatar";

export default {
  name: "MainHeader",
  components: {
    Avatar,
    LoginDialog,
    SearchInput,
    DropDown
  },
  data() {
    return {
      dropdownTitle: "课程",
      dropdownItems: ["Java", "Vue", "Python", "C++", "C#", "PHP"]
    }
  },
  methods: {
    clickCategory(item) {
      this.$router.push('/courseList/' + item.categoryId)
    },
    activeLoginDialog() {
      this.$bus.$emit("activeLoginDialog", true)
    },
    getAllCategory() {
      this.$api.category.getAllCategory()
      .then(res => {
        this.dropdownItems = res.data
      })
    },
    linkToSchoolView() {
      this.$router.push("/school")
    },
    linkToCourse() {
      this.$router.push("/courseList")
    },
    linkToProfile() {
      this.$router.push("/profile")
    },
    linkToTeacher() {
      this.$router.push("/teacher")
    },
    linkToLCourse() {
      this.$router.push("/liveCourse")
    },
    logout() {
      this.$api.account.logout()
      .then(res => {
        localStorage.removeItem("accessToken")
        this.$store.commit("setToken", null)
        this.$store.commit("setAccount", null)
        this.$message.success(res.message)
      })
      this.$router.push("/home")
    },
    changeAccount() {
      this.logout()
      this.$router.push("/login")
    }
  },
  computed: {
  },
  created() {
    this.getAllCategory()
  }
}
</script>

<style scoped>

#main-header {
  left: 0;
  top: 0;
  width: 1200px;
  height: 64px;
  border-radius: 0;
  position: relative;
  clear: none;
  display: block;
  min-width: 0;
  color: black;
  font-size: 16px;
  background-color: white;
  margin: 0 auto;
  padding: 0;
}

#main-header img {
  margin-top: 15px;
  border-radius: 0;
  height: 32px;
  vertical-align: middle;
  border-style: none;
}

#drop-down {
  margin-top: 20px;
}

#search-input {
  margin-top: 13px;
}

.el-col {
  text-align: center;
}

.content {
  display: flex;
}

.el-button {
  margin-top: 11px;
  font-size: 16px;
  color: black;
  flex: 1;
}
</style>
