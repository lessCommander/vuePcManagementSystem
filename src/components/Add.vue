<template>
<div class="add">
  <div class="container">
    <h2>添加电脑</h2>
    <div class="well">
        <div class="h3">电脑品牌信息</div>
        <div class="form-group">
            <label for="inp1" class="control-label">品牌</label>
            <input type="text" id="inp1" class="form-control" placeholder="name" v-model="PCData.brand">
        </div>
        <div class="form-group">
            <label for="inp2" class="control-label">型号</label>
            <input type="text" id="inp2" class="form-control" placeholder="type" v-model="PCData.type">
        </div>
        <div class="form-group">
            <label for="inp3" class="control-label">价格</label>
            <input type="number" id="inp3" class="form-control" placeholder="price" v-model.number="PCData.price">
        </div>
        <div class="form-group">
            <label for="inp4" class="control-label">生产日期</label>
            <input type="text" id="inp4" class="form-control" placeholder="date" v-model="PCData.date">
        </div>
        <div class="form-group">
            <label for="txtarea" class="control-label">产品简介</label>
            <textarea id="txtarea" cols="30" rows="10" class="form-control" placeholder="description" v-model="PCData.description"></textarea>
        </div>
    </div>
    <div class="form-group pull-right">
        <button class="btn btn-primary" @click="addPCData()">确认</button>
        <button class="btn btn-danger" @click="cancelPCData()">取消</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'add',
  data () {
    return {
      PCData: {
          brand: '',
          type: '',
          price: 0,
          date: '',
          description: ''
      }
    }
  },
  methods:{
    addPCData() {
        let newData = {...this.PCData};

        this.axios({
            method: 'post',
            url: 'http://localhost:3000/computers',
            data: newData
        })
        .then(res => this.$router.push({
            name: 'home',
            params:{
                info: '添加电脑信息成功！'
            }
        }));
    },
    cancelPCData(){
      this.$router.push('/');
    }
  }
}
</script>

<style scoped>

</style>
