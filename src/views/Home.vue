<template>
  <div id="home">
    <h1>MarketDial Address Book</h1>
    <AddContact v-on:add-contact="addContact"/>
    <Contacts v-bind:contacts="contacts"/>
    <!-- <Contacts v-bind:contacts="contacts" v-on:del-contact="deleteContact"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
import ContactService from '@/services/ContactService'
import Contacts from '@/components/Contacts'
import AddContact from '@/components/AddContact'
import axios from 'axios'

export default {
  name: 'home',
  components: {
    Contacts,
    AddContact
  },
  data () {
    return {
      contacts: []
    }
  },
  beforeMount () {
    this.getContacts()
  },
  methods: {
    async getContacts () {
      const { data } = await ContactService.getContacts()
      this.contacts = data.contacts
    },
    async addContact (newContact) {
      const { name, email, phone, is_favorite } = newContact
      const url = 'http://contacts-api.marketdial.com/contact'
      axios.post(url, {
        name,
        email,
        phone,
        is_favorite
      })
        .then(res => this.contacts = [...this.contacts, res.data])
        .catch(err => console.log(err))
    },
    // async deleteContact (id) {
    //   axios.delete(`http://contacts-api.marketdial.com/contacts/${id}`)
    //     .then(res => this.contacts = this.contacts.filter(contact => contact.id !== id))
    //     .catch(err => console.log(err))
    // }
  }
}
</script>

<!-- global styles -->
<style lang="sass">
  $zeroMargin: 0 auto
  #home
    max-width: 500px
    margin: 0 auto
    padding: 0 15px
</style>
