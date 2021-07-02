<template>
  <Header/>
    
  <button class="btn btn-sm btn-primary addbtn" @click="addItem">AddItem</button>

  <Table 
    v-if="showTable" 
    :list="list"
    :showForm="showForm" 
    :showTable="showTable"
    @updateshowForm="showForm = $event" 
    @updateshowTable="showTable = $event"
    @event="handler"
    @edit="editCurrentUser"/>

  <Formview 
   v-if="showForm" 
   :list ="list" 
   :showForm="showForm" 
   :showTable="showTable"
   :currEditItem="currEditItem"
   @updateshowForm="showForm = $event" 
   @updateshowTable="showTable = $event"  
   @nullcurrEdit="currEditItem = null"  />

 

</template>

<script>
import Header from './Header.vue';
import Table from './Table.vue';
import Formview from './Formview.vue';

export default {
    data(){
      return {
        list : [], 
        showForm : false, 
        showTable : true, 
        currDetItem : null,
        currEditItem : null, 
      }
    },
    components :{
        Header, Table, Formview
    },
    methods :{
      addItem(){
        this.showForm = true;
        this.showTable = false;
      },
      handler(params) {
        console.log("handler",params);
        this.list = this.list.filter((item) => { return params != item });
      },
      editCurrentUser(params){
        this.currEditItem = params;
        this.showForm = true;
        this.showTable = false;
      }
    }
}
</script>

<style>
.formDiv{
    position: absolute;
    left: 40%;
    z-index: 1;
}
.delDiv{
  position: absolute;
  right: 10px;
  top: 10px;
}
.addbtn{
  position: absolute;
  top: 10px;
  right: 10px;
}
</style>