<template>
  <div v-if="list.length">
    <table class="table">
      <tr>
        <td>First Name</td>
        <td>Last Name</td>
        <td>Email</td>
        <td>Gender</td>
        <td>DOB</td>
        <td>Age</td>
        <td>Phone</td>
      </tr>
      <tr v-for="item of list" :key="item.id">
        <td>{{ item.firstname }}</td>
        <td>{{ item.lastname }}</td>
        <td>{{ item.email }}</td>
        <td>{{ item.gender }}</td>
        <td>{{ item.dob }}</td>
        <td>{{ item.age }}</td>
        <td>{{ item.mob }}</td>
        
        <button class="btn btn-sm btn-primary" @click="editUser(item)">Edit</button> &nbsp; 
        <button class="btn btn-sm btn-danger" @click="deleteUser(item)">Delete</button>
        
      </tr>
    </table>
  </div>

  <div v-else class="text-center">
    No Details to show
  </div>


  <div v-show="delDialogueBox" class="delDiv p-2 border bg-light">
    Do you want to surely delete this item? <br> <br>
    <button class="btn btn-sm btn-danger" @click="deleteCurrItem">Yes</button> &nbsp;
    <button class="btn btn-sm btn-light" @click="noChange">No</button>
  </div>


</template>

<script>
export default {

    props : ['list'],
    data(){
      return{
          currDetItem : null,
          delDialogueBox : false,
          currEditItem : null,
      }
    },
    methods: {
       deleteUser(delItem){ 
         console.log("delITem",delItem);
          this.currDetItem = delItem;  
          this.delDialogueBox = true;
        }, 
        deleteCurrItem(){
        
          this.delDialogueBox = false;
          this.$emit('event', this.currDetItem);
          this.$emit('updateshowForm', false);
          this.$emit('updateshowTable', true);   

        },
        noChange(){
          this.delDialogueBox = false;
          this.currDetItem = null; 
        },
        editUser(item){
          this.currEditItem = item; 
          this.$emit('edit', this.currEditItem);
        }
    }

}
</script>

<style>

</style>