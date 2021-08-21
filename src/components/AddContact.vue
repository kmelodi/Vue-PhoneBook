<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Full Name</label>
      <input type="text" v-model="name" name="name" placeholder="Add Contact Full Name" />
    </div>
    <div class="form-control">
      <label>Phone Number</label>
      <input
        type="tel"
        v-model="number"
        name="number"
        placeholder="Add Phone number"
      />
    </div>
    <input type="submit" value="Save Contact" class="btn btn-save" />
  </form>
</template>

<script>
export default {
  //dsdsd
  name: 'AddContact',
  props: {
    editName: String,
    editNumber: String
  },
  data() {
   console.log(this.editName)
    return {
      name: this.editName,
      number: this.editNumber
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()

      if (!this.name) {
        alert('Please add Full Name')
        return
      }
      if (!this.number) {
        alert('Please add Phone Number')
        return
      }
      
      const newContact = {
        name: this.name,
        number: this.number
      }

      this.$emit('add-contact', newContact)

      this.name = ''
      this.number = ''
    },

  },
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
</style>
