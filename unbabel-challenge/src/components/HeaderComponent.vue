<template>
    <nav class="challenge-header">
        <div class="header-title"><p>{{headerTitle}}</p></div>
        <img @click="uploadData()" class="uplaod-btn" alt="Upload button" src="../assets/upload.svg">
        <img @click="fetchData()" class="fetch-btn" alt="Fetch data button" src="../assets/fetch-document.svg">
    </nav>
</template>

<script>
export default {
  name: 'HeaderComponent',
  props: {
    headerTitle: String
  },
  methods:{
      uploadData(){
        this.$emit("uploadData"); 
             },
      fetchData(){
        this.$emit("fetchData");
        //console.log('i am inheader');

      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
nav.challenge-header {
    display: flex;
    background-color: white;
    box-shadow: 0px 0px 3px 1px #bebec0;
    padding: 10px 100px;
    align-items: center;
}
.header-title {
    flex: 1;
}
.header-title p {
    float: left;
    font-family: "Montserrat";
    font-weight: 500;
    color: #414C5E;
}
img.uplaod-btn {
    margin-right: 20px;
    cursor: pointer;
    width: 20px;
}
img.fetch-btn {
    cursor: pointer;
    width: 20px;
}
</style>
