<template>
  <div @click="cardClick" class id="teacher-card">
    <el-card :body-style="{ padding: '0px' }" shadow="hover">
      <el-avatar :size="70" :src="teacher.teacherAvatar"></el-avatar>
      <div class="info">
        <p style="margin-top: 15px; font-size: 16px">{{teacher.teacherName}}</p>
        <p style="margin-top: 2px; font-size: 12px; color: #999">{{teacher.teacherPost}}</p>
        <p style="margin-top: 2px; font-size: 12px; color: #666">{{teacher.school.schoolName}}</p>
      </div>
    </el-card>
  </div>
</template>

<script>
export default {
  name: "TeacherCard",
  props: {
    teacher: Object
  },
  methods: {
    cardClick() {
      this.$emit("cardClick", this.teacher.teacherId)
    }
  }
}
</script>

<style scoped>
#teacher-card {
  width: 250px;
  float: left;
  margin: 10px 0;
}

.el-avatar {
  float: left;
  margin: 12px 12px;
}

.info {
  float: left;
  width: 100px;
  height: 100px;
}
</style>
