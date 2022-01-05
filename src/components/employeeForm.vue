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
      
      handleSubmit(){
      
      if(this.invalidName||this.invalidEmail){
        this.error = true;
        this.massage='you have to fill the inputs';
      }
      else{
      this.$emit('add:employee' , this.employee)
      this.$refs.first.focus()
      this.error = false;
        this.massage='done!'
      }
      },
      
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