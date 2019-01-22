<template>
    <div class="detail">
        <div class="container">
            <div class="h3">电脑配置详情</div>
            <div class="panel panel-default">
                <div class="panel-heading">{{PCData.brand}}</div>
                <div class="panel-body">
                    <table class="table table-bordered table-striped table-hover">
                        <tbody>
                            <tr>
                                <td>型号</td>
                                <td>{{PCData.type}}</td>
                            </tr>
                            <tr>
                                <td>价格</td>
                                <td>{{PCData.price}} 元</td>
                            </tr>
                            <tr>
                                <td>生产日期</td>
                                <td>{{PCData.date}}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="pull-right">
                <button class="btn btn-warning">编辑</button>
                <button class="btn btn-danger" @click="delPC">删除</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'detail',
  data() {
    return {
        PCData:{}
    }
  },
  methods: {
    showDetail() { // 初始化获取数据
        let id = this.$route.query.id;
        this.axios({
            method: 'get',
            url: 'http://localhost:3000/computers/' + id
        })
        .then(res => this.PCData = res.data);
    },
    delPC(){
        let id = this.PCData.id;
        this.axios({
            method: 'delete',
            url: 'http://localhost:3000/computers/' + id
        })
        .then(res => console.log(res));
        // ...待完成
    }
  },
  created() {
    this.showDetail();
  }
}
</script>

<style scoped>

</style>
