<template>
  <div id="app" class="small-container">
    <h1> Employees </h1>
    <employee-table
      v-bind:employees="employees"
      v-on:delete:employee="deleteEmployee"
      v-on:edit:employee="editEmployee"
    />
    <employee-form v-on:add:employee="addEmployee" />
  </div>
</template>

<script>
  import EmployeeTable from "@/components/EmployeeTable.vue"
  import EmployeeForm from "@/components/EmployeeForm.vue";

  export default {
    name: 'App',
    components: {
      EmployeeTable,
      EmployeeForm
    },
    data() {
      return {
        employees: [
          {
            id: this.genId(),
            name: "Dank Boi",
            email: "boi420@blaz.edu"
          },
          {
            id: this.genId(),
            name: "Gaymer Brian",
            email: "xxx_gaymer_xxx@steam.org"
          }
        ]
      }
    },
    methods: {
      addEmployee(employee) {
        this.employees.push({
          id: this.genId(),
          name: employee.name,
          email: employee.email
        })
      },

      deleteEmployee(id) {
        this.employees = this.employees.filter( employee => {
          return employee.id !== id;
        })
      },

      editEmployee(updatedEmployee, id) {
        this.employees = this.employees.map( employee => {
          return employee.id === id ? updatedEmployee : employee;
        })
      },

      genId() {
        return Math.floor(Math.random() * Math.floor(Date.now()))
      }
    }
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }
  .small-container {
    max-width: 680px;
  }
</style>
