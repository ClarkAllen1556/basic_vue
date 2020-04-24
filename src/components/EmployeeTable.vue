<template>
  <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">
      No dank bois
    </p>
    <table>
      <thead>
        <tr>
          <th> Name </th>
          <th> Email </th>
          <th> Actions </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" v-bind:key="employee.id">
          <td v-if="editingId === employee.id">
            <input type="text" v-model="employee.name" />
          </td>
          <td v-else> {{ employee.name }} </td>
          <td v-if="editingId === employee.id">
            <input type="text" v-model="employee.email" />
          </td>
          <td v-else> {{ employee.email }} </td>
          <td v-if="editingId == employee.id">
            <button v-on:click="editEmployee(employee)"> Save </button>
            <button v-on:click="cancelEdit(employee)" class="muted-button"> Cancel </button>
          </td>
          <td v-else>
            <button v-on:click="editMode(employee)"> Edit </button>
            <button v-on:click="$emit('delete:employee', employee.id)"> Delete </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "employee-table",
  props: {
    employees: Array
  },
  data() {
    return {
      editingId: null,
      cachedEmployee: null
    }
  },
  methods: {
    editMode(employee) {
      this.cachedEmployee = Object.assign({}, employee)
      this.editingId = employee.id
    },
    editEmployee(employee) {
      if (employee.name === '' || employee.email === '') return
      this.$emit('edit:employee', employee.id, employee)
      this.editingId = null
    },
    cancelEdit(employee) {
      Object.assign(employee, this.cachedEmployee)
      this.editingId = null;
    }
  }
}
</script>

<style scoped>
  button {
      margin: 0 0.5rem 0 0;
    }
</style>