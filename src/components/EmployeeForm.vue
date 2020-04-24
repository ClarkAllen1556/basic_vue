<template>
  <div id="employee-form">
    <form v-on:submit.prevent="handleSubmit">
      <label> Name </label>
      <input ref="first"
        v-model="employee.name"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        @focus="clearStatus"
        v-on:keypress="clearStatus"
      />
      <label> Email </label>
      <input
        v-model="employee.email"
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        @focus="clearStatus"
      />
      <p v-if="err && submitting" class="error-message">
        Fix yo shit
      </p>
      <p v-if="success" class="success-message">
        Good job you added a dank dude. Nice.
      </p>
      <button> Add cool new dude </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "employee-form",
  data() {
    return {
      submitting: false,
      err: false,
      success: false,
      employee: {
        name: "",
        email: ""
      }
    }
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();
      this.$refs.first.focus();

      if(this.invalidName || this.invalidEmail) {
        this.err = true;
        return;
      }

      this.$emit("add:employee", this.employee)

      this.err = this.success = true;
      this.submitting = false;
    },
    clearStatus() {
      this.err = this.success = false;
    }
  },
  computed: {
    invalidName() {
      return this.employee.name === "";
    },
    invalidEmail() {
      return this.employee.email === "";
    }
  }
}
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>