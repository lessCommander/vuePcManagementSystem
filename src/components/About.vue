<template>
<div class="about">
  <div class="container-fluid">
      <div class="jumbotron">
        <div class="h2">电脑信息管理系统Demo</div>
        <p>
          使用vue+bootstrap创建的简易电脑信息管理系统。
        </p>
        <button class="btn btn-lg btn-primary" @click="cancelPC()">返回主页</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'about',
  methods:{
    cancelPC(){
      this.$router.push('/');
    }
  }
}
</script>

<style scoped>

</style>
