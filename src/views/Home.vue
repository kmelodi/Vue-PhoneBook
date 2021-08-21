<template>
  <AddContact v-show=" isEditContact || showAddContact " @add-contact="addContact" :editName="this.name" :editNumber="this.number" />
  <Contacts
    @edit-contact="editContact"
    @delete-contact="deleteContact"
    :contacts="contacts"
  />
</template>

<script>
import Contacts from '../components/Contacts'
import AddContact from '../components/AddContact'
export default {
  name: 'Home',
  props: {
    showAddContact: Boolean,
  },
  components: {
    Contacts,
    AddContact,
  },
  data() {
    return {
      contacts: [],
      isEditContact:false,
      name:"",
      number:""
    }
  },
  methods: {
    async addContact(contact) {
      const res = await fetch('api/contacts', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(contact),
      })

      const data = await res.json()
      this.isEditContact = false;
      this.contacts = [...this.contacts, data]
    },
    async editContact(id) {
      if (confirm('Are you sure edit this contact?')) {
         const contactToToggle = await this.fetchContact(id)      
         const res = await fetch(`api/contacts/${id}`, {
          method: 'DELETE',
          })
          if(res.status === 200){
            this.contacts = this.contacts.filter((contact) => contact.id !== id)
            this.number = contactToToggle.number +""
            this.name = contactToToggle.name
            this.isEditContact = true   
          }else
          { 
            alert('Error deleting contact')
          }

      }
    },
    async deleteContact(id) {
      if (confirm('Are you sure remove contact?')) {
        const res = await fetch(`api/contacts/${id}`, {
          method: 'DELETE',
        })

        res.status === 200
          ? (this.contacts = this.contacts.filter((contact) => contact.id !== id))
          : alert('Error deleting contact')
      }
    },
    async fetchContacts() {
      const res = await fetch('api/contacts')

      const data = await res.json()

      return data
    },
    async fetchContact(id) {
      const res = await fetch(`api/contacts/${id}`)

      const data = await res.json()

      return data
    },
  },
  async created() {
    this.contacts = await this.fetchContacts()
  },
}
</script>
