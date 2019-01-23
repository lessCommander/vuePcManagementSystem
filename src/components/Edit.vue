<template>
<div class="edit">
  <div class="container">
    <h2>更新电脑信息</h2>
    <div class="well">
        <div class="h3 text-center">电脑信息</div>
        <form class="form-horizontal">
            <div class="form-group">
                <label for="inp1" class="control-label col-sm-2">品牌</label>
                <div class="col-sm-4">
                    <input type="text" id="inp1" class="form-control" placeholder="name" v-model="PCData.brand">
                </div>
            </div>
            <div class="form-group">
                <label for="inp2" class="control-label col-sm-2">型号</label>
                <div class="col-sm-5">
                    <input type="text" id="inp2" class="form-control" placeholder="type" v-model="PCData.type">
                </div>
            </div>
            <div class="form-group">
                <label for="inp3" class="control-label col-sm-2">价格</label>
                <div class="col-sm-4">
                    <input type="number" id="inp3" class="form-control" placeholder="price" v-model.number="PCData.price">
                </div>
            </div>
            <div class="form-group">
                <label for="inp4" class="control-label col-sm-2">生产日期</label>
                <div class="col-sm-4">
                    <input type="date" id="inp4" class="form-control" placeholder="date" v-model="PCData.date">
                </div>
            </div>
            <div class="form-group">
                <label for="txtarea" class="control-label col-sm-2">产品简介</label>
                <div class="col-sm-10">
                    <textarea id="txtarea" cols="30" rows="5" class="form-control" placeholder="description" v-model="PCData.description"></textarea>
                </div>
            </div>
        </form>
    </div>
    <div class="form-group pull-right">
        <button class="btn btn-primary" @click="addPCData()">确认</button>
        <button class="btn btn-danger" @click="cancelPC()">取消</button>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'edit',
  data () {
    return {
      PCData: {}
    }
  },
  methods:{
    setPCData(){ // 获取点击编辑按钮时，根据电脑产品的id，获取详细信息
        let id = this.$route.params.id;

        this.axios({
            method: 'get',
            url: 'http://localhost:3000/computers/' + id
        })
        .then(res => {
            this.PCData = res.data;
        });
    },
    addPCData() {
        let newData = {...this.PCData},
            id = this.$route.params.id;

        this.axios({
            method: 'put',
            url: 'http://localhost:3000/computers/' + id,
            data: newData
        })
        .then(res => this.$router.push({
            name: 'home',
            params:{
                type: 'add',
                info: '更新电脑信息成功！'
            }
        }));
    },
    cancelPC(){
      this.$router.push('/');
    }
  },
  created(){
    this.setPCData();
  }
}
</script>

<style scoped>

</style>
