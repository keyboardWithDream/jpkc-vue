<template>
  <div id="teacher">
    <div class="title">
      <div class="gl-1"></div><span>所有教师</span>
    </div>
    <div class="teacher-list">
      <div class="card" v-for="teacher in teacherList">
        <teacher-card :teacher="teacher" @cardClick="cardClick"/>
      </div>
      <div class="empty" style="visibility: hidden"></div>
      <div class="empty" style="visibility: hidden"></div>
      <div class="empty" style="visibility: hidden"></div>
    </div>
    <page-control :page-info="pageInfo"/>
  </div>
</template>

<script>
import TeacherCard from "@/components/common/TeacherCard";
import PageControl from "@/components/common/PageControl";

export default {
  name: "Teacher",
  components: {PageControl, TeacherCard},
  data() {
    return {
      pageInfo: {
        current: 1,
        size: 25,
        total: 0,
        pages: 0,
      },
      teacherList: []
    }
  },
  methods: {
    getTeacher(current, size) {
      this.$api.teacher.getAll(current, size)
      .then(res => {
        this.teacherList = res.data.list
        this.pageInfo.total = res.data.total
        this.pageInfo.pages = res.data.pages
      })
    },
    cardClick(teacherId) {
      this.$router.push("/teacher/" + teacherId)
    }
  },
  created() {
    this.getTeacher(this.pageInfo.current, this.pageInfo.size)
  }
}
</script>

<style scoped>
#teacher {
  margin: 0 auto;
  border-radius: 8px;
  width: 1200px;
}

.title {
  font-size: 24px;
  color: #666;
}

.gl-1 {
  margin-left: 20px;
  margin-right: 10px;
  float: left;
  height: 35px;
  background-color: #00c758;
  width: 3px;
}

.teacher-list {
  margin-top: 20px;
  display: flex;
  display: -webkit-flex;
  justify-content: space-between;
  flex-direction: row;
  flex-wrap: wrap;
}

.empty {
  width: 250px;
  height: 0;
  background-color: #ededed;
}
</style>
