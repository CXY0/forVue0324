<template>
  <div class="hello">
    <h1>{{ message }}</h1>
    <input type='text' placeholder='添加代办事件,按回车键确认'  @keyup.enter="enterFn" v-model="todo"/>
    
    
  <h5>未完成事件</h5>
   <ul>
    <li v-for='item in list' :key="item.title">
     <input type='checkbox' @click='setComplete(item)'/>{{item.title}}
     <button class="bSt" v-show="isShow" @click="deleteItem(item)">删除</button>
    </li>
    
    </ul>
    <h5>已完成事件</h5>
    <ul>
    <li v-for='item in list1' :key="item.title">
     <span>{{item.title}}</span><span>{{item.time}}</span>
    </li>
    
    </ul> 
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return {
      
       list:[],
       list1:[],
       message: '代办事件记录',
       todo:'',
       isShow:true
    }
  },
  methods:{
    enterFn(){
     if(this.todo==""){return;}
     this.list.push({
      title:this.todo,
      isComplete:false
     });
     this.todo = "";
    },
    setComplete(item){
      var index = this.list.indexOf(item);
      this.list.splice(index,1);
      //item.isComplete = true;
      var now = new Date();
      var y = now.getFullYear();
      var m = now.getMonth()+1;
      var d = now.getDate();
      this.list1.push({
      title:item.title,
      time:y+'-'+m+'-'+d,
     })
     
    },
    deleteItem(item){
     var index = this.list.indexOf(item);
              this.list.splice(index,1)
    },
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.bSt{
  margin-left: auto;
     }
ul{
  padding-left:0;
  width:200px;
}
li{
  list-style: none;
  display:flex;
  justify-content:space-between;
  padding-bottom: 5px;
}
</style>
