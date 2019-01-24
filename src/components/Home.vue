<template>
<div class="home">
  <div class="container">
    <alert v-if="alertTxt != ''" :alert-msg="alertTxt" :alert-type="alertType" @dismiss="closeAlert"></alert>
    <h2 class="text-center">个人电脑管理系统</h2>
    <div class="form-group">
      <div class="row">
        <div class="col-md-8 col-sm-10 col-xs-9">
          <input type="text" class="form-control" placeholder="搜索品牌" v-model="searchTxt">
        </div>
        <div class="col-md-2 hidden-sm hidden-xs"></div>
        <div class="col-md-2 col-sm-2 col-xs-3">
          <button class="btn btn-primary form-control" v-on:click="AddPC()">添加品牌</button>
        </div>
      </div>
    </div>
    <table class="table table-bordered table-striped table-hover">
      <thead>
        <tr class="info text-primary">
          <th>品牌</th>
          <th>型号</th>
          <th class="text-center">价格</th>
          <th class="text-center">操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(pc, inx) in filterLists" :key="inx">
          <td>{{pc.brand}}</td>
          <td>{{pc.type}}</td>
          <td class="text-center">{{pc.price}} 元</td>
          <td class="text-center">
            <button class="btn btn-success" @click="showDetails(inx)">详情</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
</template>

<script>
import alert from './Alert.vue';

export default {
  name: 'home',
  data () {
    return {
      lists: [],
      searchTxt: '',
      alertTxt: '',
      alertType: 'add'
    }
  },
  computed:{ // 搜索过滤后的列表
    filterLists(){
      let self = this;
      if(this.lists.length !== 0){
        return this.lists.filter(function(val){
          return val.brand.toLowerCase().match(self.searchTxt.toLowerCase());
        });
      }
    }
  },
  methods:{
    getPCData(){ // 获取数据
      this.axios.get('http://localhost:3000/computers')
        .then(response => this.lists = response.data);
    },
    AddPC(){ // 添加数据按钮触发的事件
      this.$router.push('/add');
    },
    AddSuccess(){ // 添加或删除数据成功后返回的数据
      let {type, info} = this.$route.params;
      if(info){
        [this.alertTxt, this.alertType] = [info, type];
      }
    },
    closeAlert(){ // 关闭alert警告框
      this.alertTxt = '';
    },
    showDetails(inx){ // 点击详情按钮触发事件
      let id = this.lists[inx].id;
      this.$router.push({
        path: '/detail',
        query: {
          id
        }
      });
    }
  },
  created(){
    this.getPCData();
    this.AddSuccess();
  },
  components:{
    alert
  }
}
</script>

<style scoped>
  td{
    line-height: 33px !important;
  }
</style>
