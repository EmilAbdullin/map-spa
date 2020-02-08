<template>
  <div id="app">
    <h1 class="main-heading">Application for calculationg distance between two cities</h1>
    <Map/>
    <listCalcForm
      v-bind:currentForms="currentForms"
      v-on:addNewForm="addNewForm"
      v-on:addlog="createNewLog"
    />
    <div class="separator"></div>
    <logBook
    v-bind:logs="logs"
    />
  </div>
</template>

<script>
import Map from '@/components/Map'
import listCalcForm from "@/components/listCalcForm"
import logBook from '@/components/logBook'
export default {
  name:'app',
  data(){
    return{
      forms:[
        {id:1,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point c',secondPlaceholder:'Point d',disabled:true},
        {id:2,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point e',secondPlaceholder:'Point f',disabled:false},
        {id:3,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point g',secondPlaceholder:'Point h',disabled:true},
        {id:4,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point i',secondPlaceholder:'Point j',disabled:false},
        {id:5,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point k',secondPlaceholder:'Point l',disabled:false},
        {id:6,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point m',secondPlaceholder:'Point n',disabled:false},
        {id:7,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point o',secondPlaceholder:'Point p',disabled:true},
        {id:8,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point q',secondPlaceholder:'Point r',disabled:false},
        {id:9,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point s',secondPlaceholder:'Point t',disabled:false}
      ],
      currentForms:[
        {id:0,firstPointValue:'Москва',secondPointValue:'Петербург',firstPlaceholder:'Point a',secondPlaceholder:'Point b',disabled:false}
      ],
      logs:[]
    }
  },
  components: {
    Map,listCalcForm,logBook
  },
  methods:{
      addNewForm(){
        if(typeof this.forms[0] !== 'undefined'){
          this.currentForms.push(this.forms[0]);
          this.forms.shift();
        }else{
          alert('Извините но вы не можете добавлять более 10-ти форм');
          return false;
        }
      },
      createNewLog(log){
        this.logs.push(log);
      }
  }
}
</script>

<style>

*{
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width:100%;
  height: 100%;
}
.main-heading{
  color:#3C4043;
}
.separator{
  width:95%;
  border:1px solid #ececec;
  margin:25px auto;
}

</style>



