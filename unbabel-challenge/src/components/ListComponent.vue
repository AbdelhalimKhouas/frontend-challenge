<template v-if="loaded==true">
    <div id="list-container">
        <div class="list-item" v-for="item in data" v-bind:key="item.id">
            <div class="flex">
                <p class="checkbpx-wrapper">
                <input type="checkbox" :id="'checkbox'+item.id">
                <label :for="'checkbox'+item.id"></label>
                </p>
                <img class="person" src="../assets/person.svg"/>
                <p class="item-title">{{ item.voice }}</p>
            </div>
            <p class="item-description">{{ item.text }}</p>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ListComponent',
  props:{
    data: Array,
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
    margin-left: 90px;
    margin-top: 0;
    text-align: left;
    font-family: "Open Sans";
    font-size: 16px;
    color: #778195
}













[type="checkbox"]:not(:checked),
[type="checkbox"]:checked {
  left: -99999999999px;
  position: absolute;
}
[type="checkbox"]:not(:checked) + label,
[type="checkbox"]:checked + label {
  position: relative;
  padding-left: 1.95em;
  cursor: pointer;
}
[type="checkbox"]:not(:checked) + label:before,
[type="checkbox"]:checked + label:before {
  content: '';
  position: absolute;
  left: 0; top: 0;
  width: 1.25em; height: 1.25em;
  border: 2px solid red;
  background: #fff;
  border-radius: 4px;
  box-shadow: inset 0 1px 3px rgba(0,0,0,.1);
}
[type="checkbox"]:not(:checked) + label:after,
[type="checkbox"]:checked + label:after {
  content: '\2713\0020';
  position: absolute;
  top: .15em; left: .22em;
  font-size: 1.3em;
  line-height: 0.8;
  color: #09ad7e;
  transition: all .2s;
  font-family: 'Lucida Sans Unicode', 'Arial Unicode MS', Arial;
}
/* checked mark aspect changes */
[type="checkbox"]:not(:checked) + label:after {
  opacity: 0;
  transform: scale(0);
}
[type="checkbox"]:checked + label:after {
  opacity: 1;
  transform: scale(1);
}

/* accessibility */
[type="checkbox"]:checked:focus + label:before,
[type="checkbox"]:not(:checked):focus + label:before {
  border: 2px dotted blue;
}

/* hover style just for information */
label:before {
  border: 2px solid #4778d9!important;
}
</style>
