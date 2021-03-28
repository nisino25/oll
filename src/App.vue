<template>
<h1 style="text-align:center">OLL Algorithm</h1>
<span style="margin-left:15px">{{selectedNum}} / 56 selected</span>

<div v-if="currentMenu === 'selecting'">


  <button style="float:right; margin-top:-15px; margin-right:15px" v-if="selectedNum!== 0" @click="goingToPractice">Go to practice</button>
  <button style="float:right; margin-top:-15px; margin-right:15px" v-else>Select Something</button>
  <div style="clear:both"></div>
  <hr style="clar:both">

  <div style=" clear: both"></div>
  <p>Line Cases ( {{availableCounters.line}} / 15 )</p>
  <div  v-for="(oll,i) in ollList" :key="i" > 

    <div v-if="i >= 15 && i <= 29" class="ollBox" :class="[oll.avialblity ? '' : 'opacityOn']" @click="oll.avialblity = !oll.avialblity"> 
      <!-- <span>{{oll.No}}</span> -->
      <img :src="oll.imgLink" style="width:65px">
    </div>
    
  </div>


  <div style=" clear: both"></div>
  <p>All oriented group ( {{availableCounters.oriented}} / 7 )</p>
  <div  v-for="(oll,i) in ollList" :key="i" style=""> 

    <div v-if="i >= 0 && i <= 6" class="ollBox" :class="[oll.avialblity ? '' : 'opacityOn']" @click="oll.avialblity = !oll.avialblity"> 
      <!-- <span>{{oll.No}}</span> -->
      <img :src="oll.imgLink" style="width:65px">
    </div>
    
  </div>

  <div style=" clear: both"></div>
  <p>Dot Cases ( {{availableCounters.dot}} / 8 )</p>
  <div  v-for="(oll,i) in ollList" :key="i" > 

    <div v-if="i >= 7 && i <= 14" class="ollBox" :class="[oll.avialblity ? '' : 'opacityOn']" @click="oll.avialblity = !oll.avialblity"> 
      <!-- <span>{{oll.No}}</span> -->
      <img :src="oll.imgLink" style="width:65px">
    </div>
    
  </div>

  
</div>

<div v-if="currentMenu === 'practice'" @click="currnetIndex++" style="height:400px">
  <button style="float:right; margin-top:-15px; margin-right:15px" @click="currentMenu ='selecting'">Go back to selecting</button>
  <div style="clear:both"></div>
  
  <!-- <button >Go to next</button> -->
  <hr>
  <p>Algorithm ( {{currnetIndex +1}} / 300 )</p>

  <p style="font-size:150%">{{ollShuffleList[practiceList[currnetIndex]][1] }}</p>




  <!-- <p>{{practiceList}}</p> -->
</div>



</template>





<script>
import { ollList } from './const/oll.js'
import { ollShuffleList } from './const/ollShuffle.js'

export default {
  name: 'App',

  data(){
    return {
      ollList: ollList,
      ollShuffleList: ollShuffleList,

      currentMenu: 'selecting',
      practiceList: [],
      currnetIndex: 0,
      randomIndex: 0,
    }

  },

  computed:{

    selectedNum(){
      let count = 0;
      let trueCount = 0

      while(count < this.ollList.length){
        if(this.ollList[count].avialblity){
          trueCount++
        }
        count++
      }
      return trueCount
    },

    availableCounters(){
      let list =  {
        oriented: 0, 
        dot: 0, 
        line: 0, 
        corner: 0
      }

      let count = 0
      
      while( count < this.ollList.length){
        if(this.ollList[count].avialblity){
          if(this.ollList[count].group === 'oriented'){
            list.oriented++
          }
          if(this.ollList[count].group === 'dot'){
            list.dot++
          }
          if(this.ollList[count].group === 'line'){
            list.line++
          }
          if(this.ollList[count].group === 'corner'){
            list. corner++
          }

        }
        count++
        
      }
    
      return list
    },

    availableList(){
      let counter = 0
      let list = []

      while(counter < this.ollList.length){
        if(this.ollList[counter].avialblity){
          list.push(counter)
        }
        counter++
      }

      return list
    }

  
  },
  methods:{
    goingToPractice(){

      this.randomIndex =  Math.floor(Math.random() * 3300) -1
      console
      this.currnetIndex = 0
      this.currentMenu = 'practice'
      this.generateList()
    },

    generateList(){
      let count = 0
      this.practiceList = []
      while(count < 300){
        this.practiceList.push( this.availableList[ Math.floor(Math.random() * this.availableList.length)])
        count++
      }
    }
  }
}
</script>

<style>

.ollBox{
  /* background-color:; */
  border: 1px solid black;
  margin-right: 2px;
  margin-bottom: 2px;
  float:left
}

.opacityOn{
  opacity: 0.3;
}

</style>
