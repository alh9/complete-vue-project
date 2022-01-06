<template>
  <div id="employee-form">
    <!-- <form @submit.prevent="handleSubmit"></form> -->
    <form @submit.prevent="doNothin" >
      <label>Employee name</label>
      <input type="text" v-model="employee.name" ref="first" @keydown.enter.stop="doFocus2" />
      <label>Employee Email</label>
      <input type="text" v-model="employee.email" ref="second" @keydown.enter.stop='handleSubmit'/>
      <p v-text="massage"></p>


      <button >Add Employee</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'employee-form',
    data() {
      return {
      massage:'',
        submitting: false,
        error: false,
        success: false,
        employee: {
          name: '',
          email: '',
        },
      }
    },
    methods:{
      doNothin(event){
        console.log(event)
        return 0
      },
      doFocus1(){
        this.$refs.first.focus()
      },
      doFocus2(){
        this.$refs.second.focus()
      },
      handleSubmit(){
        if(this.invalidName){

          this.error = true;
          this.massage='invalid name';
          this.doFocus1()
        
        }
        else if(this.invalidEmail){
          this.error = true;
          this.massage = 'invalid email'
          this.doFocus2()
        }
        else{

          this.$emit('add:employee' , this.employee)
          this.doFocus1()
          this.error = false;
          this.massage='done!'
       
        }
      },
      
    },
    mounted() { 
      this.doFocus1()
    },
    computed: {

      invalidName() {
      return this.employee.name === ''
      },
      invalidEmail() {
      return this.employee.email === ''|| !this.employee.email.includes('@')
      },
      haserror(){
      
      return this.error===true
      
      },
    },
  }
</script>


<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>