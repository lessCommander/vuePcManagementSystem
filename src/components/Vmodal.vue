<template>
    <div class="vmodal">
        <div class="modal"
            :class="{'in': isIn}"
            :style="{'display': displayType}"
            @click="close()"
        >
            <div class="modal-dialog modal-sm" v-on:click.stop>
                <div class="modal-content">
                    <div class="modal-header bg-danger">确认是否删除？</div>
                    <div class="modal-footer">
                        <button class="btn btn-danger" @click="ok()">确认删除</button>
                        <button class="btn btn-default" @click="close()">取消</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
export default {
    name: 'vmodal',
    data(){
        return {
            isIn: false,
            displayType: 'none'
        }
    },
    methods:{
        open(){
            this.displayType = 'block';
            this.isIn = true;
        },
        close(){
            this.isIn = false;
            this.displayType = 'none';
        },
        ok(){
            this.close();
            this.$parent.confirmDel();
        }
    }
}
</script>

<style>
    .modal{
        background-color: rgba(0,0,0,0.5);
    }
    .modal-content{
        overflow: hidden;
    }
</style>


