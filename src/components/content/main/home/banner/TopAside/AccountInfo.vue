<template>
  <div id="account-info">
    <div id="login" v-if="isLogin">
      <div class="avatar-login">
        <div class="login-avatar">
          <avatar :image="account.userAvatar"/>
        </div>
        <div class="username">{{account.username}}</div>
       <div class="my-class">
         <div v-for="course in cCourseList">
           <el-button style="height: 10px; margin-left: 25px" type="text" @click="linkToCourseDetail(course.courseId)">{{course.courseName}}</el-button>
         </div>
       </div>
        <div class="course-btn">
          <el-button @click="linkToFavorite" class="login-btn" size="small" type="success" round>我的课程</el-button>
        </div>
      </div>
    </div>
    <div id="logout" v-else>
      <div class="title">免费学习来自名校名师的精品课程</div>
      <div class="avatar">
        <avatar/>
      </div>
      <div class="login-btn">
        <el-button @click="activeLoginDialog" class="login-btn" size="small" type="success" round>登录/注册</el-button>
      </div>
      <div class="foot-info">网易和高等教育出版社出品</div>
    </div>
  </div>
</template>

<script>
import Avatar from "@/components/common/Avatar";

export default {
  name: "AccountInfo",
  components: {
    Avatar
  },
  data() {
    return {
      cCourseList: []
    }
  },
  methods: {
    activeLoginDialog() {
      this.$bus.$emit("activeLoginDialog", true)
    },
    getCollect() {
      this.$api.course.getCollect(1, 3)
      .then(res => {
        this.cCourseList = res.data.list
      })
    },
    linkToCourseDetail(courseId) {
      this.$router.push("/courseDetail/" + courseId)
    },
    linkToFavorite() {
      this.$router.push("/profile/favorite")
    }
  },
  computed: {
    isLogin() {
      return this.$store.state.token !== null
    },
    account() {
      return this.$store.state.accountInfo
    }
  },
  created() {
    if (localStorage.getItem("accessToken")) {
      this.getCollect()
    }
  }
}
</script>

<style scoped>
#account-info {
  position: relative;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  width: 200px;
  height: 360px;
}

#account-info div {
  width: 168px;
  text-align: center;
}

.title {
  position: absolute;
  top: 24px;
  left: 14px;
  width: 160px;
  line-height: 20px;
  color: black;
  text-align: center;
  font-size: 15px;
}

.avatar {
  position: relative;
  text-align: center;
  margin-left: 18px;
}

.login-btn {
  width: 168px;
  height: 32px;
  position: relative;
  margin-left: 8px;
  margin-top: 10px;
}

.foot-info {
  text-align: center;
  font-size: 12px;
  color: rgb(153, 153, 153);
  position: absolute;
  bottom: 20px;
  font-weight: 400;
  left: 16px;
}

.username {
  position: absolute;
  top: 120px;
  font-size: 16px;
  font-weight: 500;
  text-align: center;
  max-width: 150px;
  overflow: hidden;
  text-overflow: ellipsis;
  width-space: nowrap;
  margin-left: 25px;
}

.login-avatar {
  position: absolute;
  top: 30px;
  margin-left: 15px;
}

.course-btn {
  position: relative;
  left: 8px;
  top: 30px;
}

.my-class {
  margin-top: 30px;
}
</style>
