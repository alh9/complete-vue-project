<template>
  <div id="employee-form">
    <!-- <form @submit.prevent="handleSubmit"></form> -->
    <form @submit.prevent="handleSubmit">
      <label>Employee name</label>
      <input type="text" v-model="employee.name" ref="first"/>
      <label>Employee Email</label>
      <input type="text" v-model="employee.email"/>
      <p v-text="massage"></p>


      <button>Add Employee</button>
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
      doFocus(){
        this.$refs.first.focus()
      },
      handleSubmit(){
        if(this.invalidName){

          this.error = true;
          this.massage='invalid name';
        
        }
        else if(this.invalidEmail){
          this.error = true;
          this.massage = 'invalid email'
        }
        else{

          this.$emit('add:employee' , this.employee)
          this.doFocus()
          this.error = false;
          this.massage='done!'
       
        }
      },
      
    },
    mounted() { 
      this.doFocus()
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