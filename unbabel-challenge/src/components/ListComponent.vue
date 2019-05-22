<template>
    <div id="list-container">
        <div v-if="loading ==true">
            <img class="spinner" src="../assets/spinner.svg"/>
        </div>
        <div class="list-item" v-for="(item,index) in data" v-bind:key="item.id" v-bind:class="{'empty':(item.text === '' || item.voice === '')}">
            <div class="flex">
                <label class="container"> 
                  <input type="checkbox">
                  <span class="checkmark"></span>
                </label>

                <img class="person" src="../assets/person.svg"/>
                <p contenteditable="true" @focusout="editItem($event, 'voice', index)" class="item-title">{{ item.voice }}</p>
                <img @click="deleteItem(item.id)" class="trash" src="../assets/delete.svg"/>
            </div>
           
            <p contenteditable="true" @focusout="editItem($event, 'text', index)" class="item-description">{{ item.text }}</p>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ListComponent',
  props:{
    data: Array,
    loading: Boolean,
  },
  methods:{
    editItem(event,target, index){
       this.$emit("editItem",event,target, index); 
    },
    deleteItem(id){
      this.$emit("deleteItem", id); 
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div#list-container {
    margin: 30px 80px;
    background: white;
    padding: 20px;
}
.flex {
    display: flex;
    align-items: center;
}
div.list-item {
    list-style-type: none;
}
input#checkbox {
    height: 16px;
    width: 16px;
    color: purple;
}
p.checkbpx-wrapper {
    position: relative;
    display: block;
    margin-right: 20px;
}
p.item-title {
    font-size: 16px;
    font-family: "Montserrat";
    font-weight: 600;
    margin-left: 10px;
    color: #566074;
}
p.item-description {
    margin-left: 70px;
    margin-top: 0;
    text-align: left;
    font-family: "Open Sans";
    font-size: 16px;
    color: #778195
}
p:focus {
    outline-color: #859EFF;
    outline-style: dotted;
    outline-width: 2px;
}
img.trash {
    margin-left: auto;
    cursor: pointer;
    display: none;
}
.list-item:hover img.trash {
    display: block !important;
}
.list-item.empty .item-title, .list-item.empty .item-description {
    min-width: 30px;
    border: dotted 1px #85ffac;
}
.list-item.empty .item-title:focus, .list-item.empty .item-description:focus {
    outline: none !important;
}
.spinner{
  width: 50px;
}

/* The container */
.container {
  display: block;
  position: relative;
  min-height: 16px;
  padding-left: 35px;
  margin-bottom: 5px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 16px;
  width: 16px;
  background-color: #FFF;
  border: 2px solid #859EFF;
  border-radius: 5px;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #859EFF;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 5px;
  top: 0px;
  width: 4px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
