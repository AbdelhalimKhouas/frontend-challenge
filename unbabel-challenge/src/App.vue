<template>
  <div id="app">
    <HeaderComponent headerTitle="Transcriptions" @fetchData="fetchData" @uploadData="uploadData"/>
    <ListComponent :data="dataSource"/>
    <AddRowBtnComponent @addRow="addRow"/>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'
import ListComponent from './components/ListComponent.vue'
import AddRowBtnComponent from './components/AddRowBtnComponent.vue'
import axios from "axios";
import baseUrl from './config/environment'

const api = axios.create({
  baseURL: baseUrl
});

export default {
  name: 'app',
  components: {
    HeaderComponent,
    ListComponent,
    AddRowBtnComponent
  },
  data(){
    return{
      dataSource: [],
    }
  },
  methods: {
     async fetchData() {
      const response =  await api.get();
      console.log(response)
      this.dataSource = response.data
      console.log(this.dataSource);
    },

    async uploadData() {
      api.post("", this.dataSource);
    },

    addRow(){
      this.dataSource.push({id: new Date().getTime(), voice: "", text: "" });
    }
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:500,600&display=swap');
@import url('https://fonts.googleapis.com/css?family=Open+Sans&display=swap');

body {
    background: #f6f7f8;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 10px;
  background-color: #f6f7f8;
  box-shadow: 0px 0px 3px 1px #bebec0;
  padding-bottom: 30px;
}
</style>
