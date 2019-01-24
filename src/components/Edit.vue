<template>
<div class="edit">
  <div class="container">
    <ol class="breadcrumb">
        <li>
            <router-link to="/">主页</router-link>
        </li>
        <li>
            <a href="javascript:" @click="cancelPC()">详情</a>
        </li>
        <li class="active">更新</li>
    </ol>
    <h2>更新电脑信息</h2>
    <div class="well clearfix">
        <div class="h3 text-center">电脑信息</div>
        <form class="form-horizontal">
            <div :class="brandGroupClass">
                <label for="inp1" class="control-label col-sm-2">*品牌</label>
                <div class="col-sm-4">
                    <input type="text" id="inp1" class="form-control" placeholder="name" v-model="PCData.brand" @blur="blurfn('brand')">
                    <span :class="brandTooltipClass"></span>
                </div>
            </div>
            <div :class="typeGroupClass">
                <label for="inp2" class="control-label col-sm-2">*型号</label>
                <div class="col-sm-5">
                    <input type="text" id="inp2" class="form-control" placeholder="type" v-model="PCData.type" @blur="blurfn('type')">
                    <span :class="typeTooltipClass"></span>
                </div>
            </div>
            <div :class="priceGroupClass">
                <label for="inp3" class="control-label col-sm-2">*价格</label>
                <div class="col-sm-4">
                    <input type="number" id="inp3" class="form-control" placeholder="price" v-model.number="PCData.price" @blur="blurfn('price')">
                    <span :class="priceTooltipClass"></span>
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
        <div class="label label-danger pull-right">
            <!-- <div class="text-danger"> -->
                带星号*项不能为空！
            <!-- </div> -->
        </div>
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
      PCData: {},
      pattern: {
          brand: /.+/,
          type: /.+/,
          price: /\d+/
      },
      isIconShow: {
          brand: false,
          type: false,
          price: false
      }
    }
  },
  computed:{
    brandGroupClass(){
        return {
            'form-group': true,
            'has-feedback': this.isIconShow.brand,
            'has-error': this.isIconShow.brand,
            'has-success': !this.isIconShow.brand
        }
    },
    brandTooltipClass(){
        return {
            'glyphicon': this.isIconShow.brand,
            'form-control-feedback': this.isIconShow.brand,
            'glyphicon-remove': this.isIconShow.brand
        }
    },
    typeGroupClass(){
        return {
            'form-group': true,
            'has-feedback': this.isIconShow.type,
            'has-error': this.isIconShow.type,
            'has-success': !this.isIconShow.type
        }
    },
    typeTooltipClass(){
        return {
            'glyphicon': this.isIconShow.type,
            'form-control-feedback': this.isIconShow.type,
            'glyphicon-remove': this.isIconShow.type
        }
    },
    priceGroupClass(){
        return {
            'form-group': true,
            'has-feedback': this.isIconShow.price,
            'has-error': this.isIconShow.price,
            'has-success': !this.isIconShow.price
        }
    },
    priceTooltipClass(){
        return {
            'glyphicon': this.isIconShow.price,
            'form-control-feedback': this.isIconShow.price,
            'glyphicon-remove': this.isIconShow.price
        }
    }
  },
  methods:{
    blurfn(inputName){
        this.isIconShow[inputName] = !this.pattern[inputName].test(this.PCData[inputName]);
    },
    setPCData(){ // 根据电脑产品的id，获取详细信息
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
        // 验证表单
        for(let key in this.isIconShow){
            this.blurfn(key);
        }
        if(this.isIconShow.brand || this.isIconShow.type || this.isIconShow.price){
            return false;
        }

        //提交数据
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
        let id = this.PCData.id;
        this.$router.push({
            path: '/detail',
            query: {
                id
            }
        });
    }
  },
  created(){
    this.setPCData();
  }
}
</script>

<style scoped>

</style>
