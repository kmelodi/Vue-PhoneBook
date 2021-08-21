<template>
  <div :key="contact.id" v-for="contact in contacts">
    <Contact
      @edit-contact="$emit('edit-contact', contact.id)"
      @delete-contact="$emit('delete-contact', contact.id)"
      :contact="contact"
    />
  </div>
</template>

<script>
import Contact from './Contact'

export default {
  name: 'Contacts',
  props: {
    contacts: Array,
  },
  components: {
    Contact,
  },
  emits: ['delete-contact', 'edit-contact'],
}
</script>
