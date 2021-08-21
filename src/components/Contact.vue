<template>
  <div class="contact" >
    <h3>
      {{ contact.name }}
      <i @click="$emit('edit-contact', contact.id)" class="fas fa-edit"></i>
      <i @click="$emit('delete-contact', contact.id)" class="fas fa-times" ></i>
    </h3>
    <p>{{ contact.number }}</p>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  props: {
    contact: Object,
  },
}
</script>

<style scope>
.fas {
  color: red;
}
.fas.fa-edit {
  color: green;
}

.contact {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.contact h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

</style>
