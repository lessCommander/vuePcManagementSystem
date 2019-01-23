<template>
    <div class="detail">
        <div class="container">
            <div class="panel panel-default">
                <div class="panel-heading">
                    <div class="h4">电脑配置详情</div>
                </div>
                <div class="panel-body">
                    <table class="table table-bordered table-striped table-hover">
                        <tbody>
                            <tr>
                                <td>品牌</td>
                                <td>{{PCData.brand}}</td>
                            </tr>
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
                            <tr>
                                <td>产品简介</td>
                                <td>{{PCData.description}}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="pull-right">
                <button class="btn btn-warning" @click="editPC()">编辑</button>
                <button class="btn btn-danger" @click="delPC()">删除</button>
                <button class="btn btn-default" @click="cancelPC()">返回</button>
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
        .then(res => {
            this.$router.push({
                name: 'home',
                params: {
                    type: 'delete',
                    info: '删除电脑信息成功！'
                }
            });
        });
    },
    editPC(){
        let id = this.PCData.id;
        this.$router.push({
            name: 'edit',
            params: {
                id
            }
        });
    },
    cancelPC(){
        this.$router.push('/');
    }
  },
  created() {
    this.showDetail();
  }
}
</script>

<style scoped>

</style>
