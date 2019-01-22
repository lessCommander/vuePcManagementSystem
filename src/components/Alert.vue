<template>
<div class="alert">
    <div class="alert alert-success">
      <button class="close" @click="dismiss">
        <span>&times;</span>
      </button>
      <span>{{alertMsg}}</span>
    </div>
</div>
</template>

<script>
export default {
  name: 'alert',
  props: {
    alertMsg: {
      type: String,
      default: ''
    }
  },
  methods:{
    dismiss(){
      this.$emit('dismiss');
    }
  }
}
</script>

<style scoped>

</style>
