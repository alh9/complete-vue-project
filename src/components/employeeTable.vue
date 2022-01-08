<template>
  <div id="employee-table">
    <p v-if="employees.length<1" class="empty-table">
    "nothing to show"
    </p>
    <table v-else>
      <thead >
        <tr>
          <th :class="{darkModeText:moonIcon}">Employee name</th>
          <th :class="{darkModeText:moonIcon}">Employee email</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td v-if="editing === employee.id">
            <input type="text" v-model="employee.name" />
          </td>
          <td v-else :class="{darkModeText:moonIcon}">{{ employee.name }}</td>
          <td v-if="editing === employee.id">
            <input type="text" v-model="employee.email" />
          </td>
          <td v-else :class="{darkModeText:moonIcon}">{{ employee.email }}</td>
          <td v-if="editing === employee.id">
            <button @click="editEmployee(employee)" :class="{darkModeButton : moonIcon}">Save</button>
            <button class="muted-button" @click="cancelEdit(employee)" :class="{darkModeButton : moonIcon}">Cancel</button>
          </td>
          <td v-else>
            <button @click="editMode(employee)" :class="{darkModeButton : moonIcon}">Edit</button>
            <button @click="$emit('delete:employee', employee.id)" :class="{darkModeButton : moonIcon}">Delete</button>
          </td>
        </tr>  
      </tbody>
    </table>
  </div>
</template>


<script>
  export default {
    name: 'employee-table',
    props:{
      employees:Array,
      moonIcon:Boolean,
    },
    data() {
      return {
        editing: null,
      }
    },
    methods:{
      editMode(employee) {
        this.cachedEmployee = Object.assign({}, employee)
        this.editing = employee.id
      },
      editEmployee(employee) {
        if (employee.name === '' || employee.email === '') return
        this.$emit('edit:employee', employee.id, employee)
        this.editing = null
      },
      cancelEdit(employee) {
        Object.assign(employee, this.cachedEmployee)
        this.editing = null;
      },
    },
  }
</script>


<style scoped>
    .empty-table{
        color:red;
        font-size:35px;
        margin-left:230px;
    }
</style>