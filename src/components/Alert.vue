<template>
<div class="alert">
    <div class="alert" :class="alertType === 'add' ? 'alert-success' : 'alert-danger'">
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
    },
    alertType: {
      type: String,
      default: 'add'
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
