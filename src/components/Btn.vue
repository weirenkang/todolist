<template>
  <div class="btn">
     <div id="app">
        <input type="text" class="input1" v-model="title" @keyup.enter="add()">
        <h1>正在进行</h1>
        <ul>
            <li v-for="(item,key) in arr" v-show="!item.flag" :key="key">
                <input type="checkbox" v-model="item.flag" @change="change">
               <span v-show="!item.isshow" @click="show(key)">{{item.title}}</span>
               <input type="text"  v-model="item.title" v-show="item.isshow" @blur="save(key)">
               <button @click="del(key)"> x</button>
            </li>
        </ul>
        <h1>已经完成</h1>
        <ul>
            <li v-for="(item,key) in arr"  v-show="item.flag" :key="key">
                <input type="checkbox" v-model="item.flag" @change="change">
               <span>{{item.title}}</span>
            </li>
        </ul>
    </div>
  </div>
</template>

<script>
export default {
data(){
    return {
           title:"",
          
           arr:JSON.parse(localStorage.getItem("todo"))||[]
    }
},
methods:{
     add(){
               if(this.title==""){
                   return false
               }
                var obj ={title:this.title,flag:false,isshow:false}
               this.arr.push(obj)
                 localStorage.setItem("todo",JSON.stringify(this.arr))
                 this.title=""
            },
            change(){
                localStorage.setItem("todo",JSON.stringify(this.arr))
            },
            show(key){
                for(var i in this.arr){
                    this.arr[i].isshow=false
                }
                this.arr[key].isshow=true
            },
            save(key){
                this.arr[key].isshow=false
                localStorage.setItem("todo",JSON.stringify(this.arr))
            },
            del(key){
                this.arr.splice(key,1)
                localStorage.setItem("todo",JSON.stringify(this.arr))
            }
}
}
</script>

<style>
 .btn{
           text-align: center;
       }
       ul{
           list-style: none;
           margin: 0 auto;
       }
     
        li{
            width: 500px;
            height: 50px;
            text-align: center;
            background: pink;
            line-height: 50px;
            margin: 0 auto;
            
        }
</style>