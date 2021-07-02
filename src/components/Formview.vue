<template>
   <div class="formDiv col-md-3 border bg-light p-2">
    <i class="fa fa-close float-end" @click="closeForm"></i>
    <form @submit.prevent="handleSubmit">

        <label>First Name</label>
        <input class="form-control p-1" type="text" @change="checkFirstName" v-model="firstname" >
        <p class="alertmsg">{{ firstnameError }}</p> <br>

        <label>Last Name</label>
        <input class="form-control  p-1" type="text" @change="checkLastName" v-model="lastname" > 
        <p class="alertmsg">{{ lastnameError }}</p> <br>

        <label>Email</label>
        <input class="form-control  p-1" type="text" @change="checkEmail" v-model="email" > 
        <p class="alertmsg">{{ emailError }}</p> <br>

        <label>Gender</label> <br>
        <input  type="radio" v-model="gender" @change="checkGender" value="male">Male
        <input  type="radio" v-model="gender" @change="checkGender" value="female">Female 
        <input  type="radio" v-model="gender" @change="checkGender" value="other">Others 
        <br>
        <p class="alertmsg">{{ genderError }}</p> <br>

        <label>DOB</label>
        <input class="form-control  p-1" type="date" @change="checkDob" v-model="dob" > 
        <p class="alertmsg">{{ dobError }}</p> <br>

        <label>Age</label>
        <input class="form-control p-1" type="number" @change="checkAge" v-model="age" > 
        <p class="alertmsg">{{ ageError }}</p><br>

        <label>Phone</label>
        <input class="form-control p-1" type="text" @change="checkPhone" v-model="mob" > 
        <p class="alertmsg">{{ mobError }}</p> <br>

        <button class="btn btn-primary btn-sm">Submit</button>

  </form>
  </div>

</template>

<script>
export default {
    props : ['list', 'showForm', 'currEditItem'],
    
    mounted(){
      
        if(this.currEditItem)
        {
            console.log('not null', this.currEditItem);
            const  currItem = this.currEditItem; 
            this.firstname = currItem.firstname; 
            this.lastname = currItem.lastname; 
            this.email = currItem.email; 
            this.gender = currItem.gender; 
            this.dob = currItem.dob;
            this.age = currItem.age;
            this.mob = currItem.mob;
        }
    },
    data(){
        return{
            firstname : '', 
            lastname : '',
            email : '',
            gender: '', 
            dob : '', 
            age: '',
            mob: '',
            firstnameError : '',
            lastnameError : '',
            emailError : '',
            ageError : '',
            mobError : '',
            genderError : '',
            dobError : ''
            
        }
    },
    methods : {

        handleSubmit(){
            if(this.currEditItem)
            {
                this.list.forEach((item) => {
                console.log(item.id);
                
                if(item.id  === this.currEditItem.id)
                {

                item.firstname = this.firstname;
                item.lastname = this.lastname;
                item.email = this.email;
                item.gender = this.gender;
                item.dob = this.dob;
                item.age = this.age;
                item.mob = this.mob;
                console.log("match",item.id);
                console.log(item);
                }
                
                    this.checkFirstName();
                    this.checkLastName();
                    this.checkEmail();
                    this.checkAge();
                    this.checkPhone();
                    this.checkGender();
                    this.checkDob();

                }); 
                 if(this.firstname !== '' && this.lastname !== '' && this.dob !='' && this.email !== '' && this.mob !== '' && this.gender !== '' && this.age !== '' && this.firstnameError === '' && this.lastnameError === '' && this.emailError === '' && this.ageError === '' && this.mobError === ''){
                    //alert('here');
                    this.$emit('updateshowForm', false);
                    this.$emit('updateshowTable', true);
                    this.$emit('nullcurrEdit');
                }
                else{
                    this.checkFirstName();
                    this.checkLastName();
                    this.checkEmail();
                    this.checkAge();
                    this.checkPhone();
                    this.checkGender();
                    this.checkDob();
                }
               
            }
            else 
            {
                const currItem = { 
                firstname : this.firstname, 
                lastname : this.lastname,
                email : this.email,
                gender : this.gender, 
                dob : this.dob,
                id : this.email,
                age : this.age, 
                mob : this.mob, 
                };

                    this.checkFirstName();
                    this.checkLastName();
                    this.checkEmail();
                    this.checkAge();
                    this.checkPhone();
                    this.checkGender();
                    this.checkDob();

                 if(this.firstname !== '' && this.lastname !== '' && this.dob !='' && this.email !== '' && this.mob !== '' && this.gender !== '' && this.age !== '' && this.firstnameError === '' && this.lastnameError === '' && this.emailError === '' && this.ageError === '' && this.mobError === ''){
                    //alert('create here');
                    console.log(this.list);
                    console.log(currItem);
                    this.list.push(currItem);
                    this.$emit('updateshowForm', false);
                    this.$emit('updateshowTable', true);
                }
                else{
                    //console.log('else');
                    this.checkFirstName();
                    this.checkLastName();
                    this.checkEmail();
                    this.checkAge();
                    this.checkPhone();
                    this.checkGender();
                    this.checkDob();
                }
                
                
            }
         
        },
        closeForm(){
            this.$emit('updateshowForm', false);
            this.$emit('updateshowTable', true);
            this.$emit('nullcurrEdit');
        }, 
        checkFirstName(){
                const regex = /^[A-Za-z]+$/;
                const isValid = regex.test(this.firstname); 
                if (!isValid) {
                    this.firstnameError = "Special Characters and number is not allowed"
                } 
                else {
                    this.firstnameError = '';
                }
            
        },
        checkLastName(){
             const regex = /^[A-Za-z]+$/;
                const isValid = regex.test(this.lastname); 
                if (!isValid) {
                    this.lastnameError = "Special Characters and number is not allowed"
                } 
                else{
                    this.lastnameError = '';
                }
        },
        checkEmail(){
            const regex = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
            const isValid = regex.test(this.email); 
            if (!isValid) {
                this.emailError = "Provide valid mail";
            } 
            else{
                this.emailError = '';
            }
        },
        checkAge(){
            if(this.age > 0 && this.age <= 150){
                this.ageError = '';
            }
            else{
                this.ageError = 'Provide a valid age';
            }

        },
        checkPhone(){
            console.log(this.mob);
            if (this.mob.length !== 10) {
                this.mobError = "Provide valid phone number";
            } 
            else{
                this.mobError = '';
            }
        },
        checkGender(){
            
            if(this.gender === ''){
                this.genderError = 'Provide input';
            }
            else{
                this.genderError = '';
            }
        },
        checkDob(){
            if(this.dob === ''){
                this.dobError = 'Provide input';
            }
            else{
                this.dobError = '';
            }
        }
        
    },
    
}
</script>

<style>
.alertmsg{
    color: red;
    font-size: 10px;
}
</style>