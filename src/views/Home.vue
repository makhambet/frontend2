<template>
  <div class="home">
    <h1>Home</h1>
    <div class="choice">
      <label>Хотите изменить количество списка</label>
      <select @click="size=$event.target.value" :value="size">
      <option v-for="level in levels" :key="level">{{level}}</option>
    </select>
    </div>
    <div class="home_content">
      <div v-for="(q,i) in paginatedData" :key="i">
        <img :src="q.img" alt="">
        <p>{{q.p}}</p>
      </div>
    </div>
    <div class="clicked">
      <div class="left">
        <button :disabled="pageNumber === 0" @click.prevent="prevPage()">Предыдущая</button>
      </div>
      <div class="middle">
        <button v-if="pageNumber!==0" @click="pageNumber=0">1</button>
        <span v-if="pageNumber>=2">...</span>
        <button class="current">{{pageNumber+1}}</button>
        <span v-if="pageNumber<currentPage-2">...</span>
        <button v-if="pageNumber<currentPage-1" @click="pageNumber=currentPage-1">{{currentPage}}</button>
      </div>
      <div class="right">
        <button @click.prevent="nextPage()" :disabled="pageNumber >= pageCount -1" >Следущая</button>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import qwe from '../data.js'
import hello from '../components/Hello'
export default {
  name: 'home',
  data() {
    return {
      qwe: qwe.data,
      pageNumber: 0,
      size: 8,
      length: qwe.data.length,
      levels: [2,3,4,6,8,12,16,24],
      start: 0,
      end: 0
    }
  },
  computed: {
    paginatedData() {
      const start = this.pageNumber * this.size,
            end = start*1.0 + this.size*1.0;
      return this.qwe.slice(start, end);
    },
    pageCount(){
      let l = this.qwe.length,
          s = this.size;
      return Math.floor(l/s);
    },
    currentPage(){
      return Math.floor(this.length/this.size)
    }
  },
  methods: {
    prevPage(){
      return this.pageNumber--
    },
    nextPage(){
      return this.pageNumber++
    },
  },
  created(){
    
  },
  components: {
    hello
  },
  watch:{
    qwe(){
      const start = this.pageNumber * this.size;
      const end = start + this.size;
    }
  }
}
</script>
<style scope>
  h1{
    text-align: center;
    font-size: 40px;
  }
  .choice{
    margin: 0 0 3% 35%;
  }
  label{
    font-size: 20px;
    margin-right: 2%;
  }
  select{
    font-size: 16px;
  }
  .home{
    width: 80%;
    margin: 0 auto;
  }
  .home_content >div:nth-child(1){
    grid-area: a;
  }
  .home_content >div:nth-child(2){
    grid-area: b;
  }
  .home_content >div:nth-child(3){
    grid-area: c;
  }
  .home_content >div:nth-child(4){
    grid-area: d;
  }
  .home_content{
    display: grid;
    grid-template-areas: "a b c d";
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 20px;
  }
  .home_content > div{
    background: #fff;
  }
  .home_content > div img{
    width: 100%;
  }
  .home_content > div p{
    font-size: 20px;
    color: #999;
    text-align: center;
  }
  .home .clicked{
    width: 60%;
    margin: 40px auto;
    display: flex;
    justify-content: space-between
  }
  .home .clicked button, .home .clicked .current{
    padding: 0 20px;
    max-width: 160px;
    background-color: transparent;
    border-radius: 4px;
    border: 1px solid #ccc;
    text-decoration: none;
    margin: 0 6px;
    transition: all .2s ease-in-out;
  }
  .home .clicked button, .home .clicked span {
    text-align: center;
    font-family: Helvetica, Arial, sans-serif;
    font-weight: 300;
    line-height: 42px;
    height: 44px;
    color: #999;
    font-size: 18px;
  }
  .home .clicked button:hover {
    border-color: #ea4c89;
    color: #ea4c89;
  }
  .home .clicked .current {
    border-color: #ea4c89;
    color: #ea4c89;
  }
</style>