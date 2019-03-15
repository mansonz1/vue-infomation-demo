<template id="demos">
    <div class="overlay" v-show="isactive"><!--v-show-->
        <h4>新增 | 修改</h4>
        <input type="text" id="text" v-model="modifylist.name" >
        <input type="button" value="取消" @click="changeActive" id="cancle">
        <input type="button" @click="modify" value="保存" id="confirm">
    </div>
</template>

<script>
    export default {
        props: [ "list","isactive"],
        computed:{
            modifylist(){
                return this.list;
            }
        },
        methods:{
            changeActive(){
                this.$emit("change")
            },
            modify(){
                if(this.modifylist.name == ""){
                    alert("the new name imputed can't be empty");
                    /*this.$emit("change")*/
                }else{
                    this.$emit("modify",this.modifylist);
                }
            }
        }
    }
</script>

<style scoped>
    .overlay{
        position:relative;
        width:250px;
        height:130px;
        border:1px solid darkgray;
        background-color: white;
        left:50px;
        top:-20px;
        opacity: 0.8;
    }
    h4{position:relative;top:20px;left:85px;}
    #cancle,#confirm{position:relative;top:70px;left:-53px;margin-left:10px;width:50px;}
    #text{position:relative;top:30px;left:72px;width:100px;height:25px;font-size:15px;text-align:center;}
</style>