<template>
  <div id="app">
    <HeaderComponent headerTitle="Transcriptions" @fetchData="fetchData" @uploadData="uploadData"/>
    <ListComponent :data="dataSource" :loading="loading" @editItem="editItem" @deleteItem="deleteItem"/>
    <AddRowBtnComponent @addRow="addRow"/>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'
import ListComponent from './components/ListComponent.vue'
import AddRowBtnComponent from './components/AddRowBtnComponent.vue'
import axios from "axios";
import baseUrl from './config/environment'

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
      loading: false
    }
  },
  methods: {
    fetchData() {
      //Fetching data from the given endpoint and save it to dataSource
      //Adding a loader when fetching for UX
      this.loading = true
      axios.get(baseUrl)
      .then((response) => {
        this.loading = false
        this.dataSource = response.data
      })
      .catch(function (error) {
        
        console.log(error);
      });
    },

    uploadData() {
      //Upload the latest data (dataSource) to the given endpoint
      //Displaying spinner when click upload to make interaction with user
      this.loading = true
      axios.post(baseUrl, {
        data: this.dataSource
      })
      .then((response) => {
        this.loading = false
        console.log('Data has been sent')
      })
      .catch(function (error) {
        console.log(error);
      });
    },

    editItem($event,target, index){
      //Editing dataSource element according to its index passed from ListComponent
      this.dataSource[index][target] = $event.target.innerText;
      //To avoide the input displaying the text twice when fisrt time added and edited we remove the inserted content at first
      $event.target.innerText = "" + $event.target.innerText
    },

    deleteItem(id){
      //Find the index of the element using its id then remove it from the array
      this.dataSource.splice(this.dataSource.findIndex(item => item.id === id), 1);
      console.log( this.dataSource)
    },
    addRow(){
      //Push a new item in dataSource
      //I set the id to timestamp to insure it will be unique
      console.log('i am add: ')
      console.log(this.dataSource)
      this.dataSource.push({id: new Date().getTime(), voice: '', text: '' });
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
