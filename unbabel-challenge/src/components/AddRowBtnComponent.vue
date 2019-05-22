<template>
        <img @click="addRow()" class="add-btn" alt="Add row" src="../assets/add-row.svg">
</template>

<script>
export default {
  name: 'AddRowBtnComponent',

  methods:{
      addRow(){
            //send addRow event to App
            this.$emit("addRow");
            },
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
img.add-btn {
    cursor: pointer;
}
img.add-btn:hover {
   transform: scale(1.2);
}
</style>
