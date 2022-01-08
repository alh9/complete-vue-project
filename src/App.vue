<template>
  <div id="app" class="small-container" :class="{darkModeContainer : moonIcon}">
    <employee-form @add:employee="addEmployee" :moonIcon="moonIcon"/>
    <div class="modeButton" @click='changeMode' :class="{moon : moonIcon}"></div>
    <br>
    <h1 :class="{darkModeText:moonIcon}">Employees</h1>
    <employee-table 
      :moonIcon="moonIcon"
      :employees="employees" 
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee"      
    />
  </div>
</template>

<script>
  import employeeTable from './components/employeeTable.vue'
  import employeeForm from './components/employeeForm.vue'
  export default {
    name: 'App',
    components: {
      employeeTable,
      employeeForm,
    },
    data(){

      return {
        darkMode: false,
        moonIcon: false ,  
        employees: [
          {
            id: 1,
            name: 'Richard Hendricks',
            email: 'richard@piedpiper.com',
          },
          {
            id: 2,
            name: 'Bertram Gilfoyle',
            email: 'gilfoyle@piedpiper.com',
          },
          {
            id: 3,
            name: 'Dinesh Chugtai',
            email: 'dinesh@piedpiper.com',
          },
        ],
      }
    },
    methods:{
      changeMode(){
        if(!this.moonIcon){//turns to dark
          this.moonIcon = true; 
          document.body.classList.add('darkModeBody') 
        }
        else{//turns to light
          this.moonIcon = false;
          document.body.classList.remove('darkModeBody')
        }      
      },
      addEmployee(employee) {
        const lastId =
        this.employees.length > 0
        ? this.employees[this.employees.length - 1].id//don't use index of 'for' for :key //we use filter just for arrays
        : 0;
        const id = lastId + 1;
        const newEmployee = { ...employee, id };
        this.employees = [...this.employees, newEmployee];
      },
      deleteEmployee(id) {  
        this.employees = this.employees.filter(
        employee => employee.id !== id
        )
      },
      editEmployee(newEmployee,id){
        this.employees = this.employees.map(employee =>
        employee.id === id ? newEmployee : employee
        )
      }
    },
    
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }
  .small-container {
    max-width: 680px;
    background-color: #fff;
  }
  body{
    background-color: #fff;
    /*background-image: url('assets/crescentMoon.png');*/
  }
  .darkModeBody{
    background-color: grey;
  }
  .darkModeContainer{
    background-color: #303134;
  }
  .darkModeText{
    color: white;
  }
  .darkModeButton{
    background-color: yellow;
  }
  .lightModeButton{
    background-color:#009435 ;
  }
  .modeButton{
    background-color: black;
    width: 100px;
    height: 100px;
    border-radius: 50px;
    margin: auto;
    background-image:url('assets/sun.jpg');
    background-size: 100px;
    cursor: pointer;
  }
  .moon{
    background-image:url('assets/crescentMoon.png');
    background-size: 100px;
  }
</style>
