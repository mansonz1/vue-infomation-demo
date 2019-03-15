<template>
  <div id="wrapper">
    <div id="a">
    <img src="../img/timg.jpg" alt="">
    <div id="new" @click="add()">新增</div>
    <table>
      <tr>
        <th>姓名</th>
        <th>操作</th>
      </tr>
      <tr v-cloak v-for="(item,index) of list">
        <td>{{item.name}}</td>
        <td><a href="javascript:;" @click="showInfo(index)">编辑</a>&nbsp&nbsp<a href="javascript:;" @click="del(index)">删除</a></td>
      </tr>
    </table>
    <model :list="selectedlist" :isactive="isActive" v-cloak @change="changeOverlay" @modify="modify"></model>
  </div>
  </div>
</template>

<script>
  import model from "@/components/model";
  import Vue from "vue";
export default {
  name: 'App',
  data(){
    return{
      isActive:false,
      selected:-1,
      selectedlist:{},
      slist:[],
      searchlist:[],
      list:[{
        name:"Jack",
      },{
        name:"Joe"
      },{
        name:"Tom"
      }],
      demoss:"name"
    }
  },
  created(){
    this.setSlist(this.list);
  },
  methods:{
    del(index){
      this.list.splice(index,1);
      this.setSlist(this.list);
    },
    setSlist(arr){
      this.slist = JSON.parse(JSON.stringify(arr));
    },
    modify(arr){
      if(this.selected > -1){
        Vue.set(this.list,this.selected,arr);
        this.selected = -1;
      }else{
        this.list.push(arr);
      }
      this.setSlist(this.list);
      this.changeOverlay();
    },
    add(){
      console.log("新增");
      this.selectedlist = {
        name:"",
      };
      this.selected = -1;
      this.isActive = true;
    },
    changeOverlay(){
      this.isActive = !this.isActive;
    },
    showInfo(index){
      this.selected = index;
      this.selectedlist = this.list[index];
      this.changeOverlay();
    }
  },
  components:{
    model
  }
}
</script>

<style>
  *{padding:0;margin:0;}
  [v-cloak]{display:none}
  #a{border:1px solid darkgray;
  width:350px;
  height:600px;
  position:relative;
  top:200px;}
  body,html{display:flex;justify-content: center;align-items: center;}
  #wrapper{
    display:flex;justify-content: center;align-items: center;
  }
  img{width:280px;position:relative;top:25px;left:35px;}
  #new{
    border:1px solid forestgreen;
    width:200px;
    height:30px;
    border-radius: 5px 5px 5px 5px;
    text-align:center;
    line-height:30px;
    color:white;
    font-size:14px;
    position:relative;
    left:70px;
    top:45px;
    background-color: seagreen;
  }
  #new:hover{
    cursor:pointer;
    text-decoration: underline;
    color:darkblue;
  }
  table{/*border:1px solid darkgray;*/position:relative;top:60px;}
  th{/*border:1px solid black;*/width:200px;font-size:14px;color:midnightblue}
  td{text-align:center;font-size:13px;color:midnightblue;}
  a{text-decoration: none;color:midnightblue;}

</style>

