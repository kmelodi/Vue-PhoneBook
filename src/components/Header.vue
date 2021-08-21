<template>
<div class="logo">
  <img class="image" alt="Tajan System" src="../assets/tajan.png">
  <h3>Tajan System</h3>
</div>
  <header>

    <h1>{{ title }}</h1>
    <Button
      v-show="homePage"
      @btn-click="$emit('toggle-add-contact')"
      :text="showAddContact ? 'Close' : 'Add Contact'"
      :color="showAddContact ? 'red' : 'green'"
    />
  </header>
</template>

<script>
import Button from './Button'

export default {
  name: 'Header',
  props: {
    title: String,
    showAddContact: Boolean,
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      if (this.$route.path === '/') {
        return true
      } else {
        return false
      }
    },
  },
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.logo{
  text-align: center;
  border-bottom: 2px solid steelblue;
  margin: 10px;
  padding: 10px;
}
 .image{
  min-height: 80px; 
 } 
</style>
