<template>
    <div class="form-container">
        <form @submit="addContact">
            <div>
                <label for="name">Full Name:</label>
                <input type="text" v-model="name" id="name" name="name" required>
            </div>
            <div>
                <label for="email">Email:</label>
                <input type="email" v-model="email" id="email" name="email">
            </div>

            <div>
                <label for="phone">Phone Number:</label>
                <input type="tel" v-model="phone" id="phone" name="phone">
            </div>
            <div class="checkbox-container">
                <input type="checkbox" v-model="isFavorite" id="favorite" name="is_favorite">
                <label for="favorite">Favorite Contact?</label>
            </div>
            <div class="submit-container">
                <button class="btn">Add Contact</button>
            </div>
        </form>
    </div>
</template>
<script>
export default {
  name: 'AddContact',
  data () {
    return {
      name: this.name,
      email: this.email,
      phone: this.phone,
      isFavorite: this.is_favorite
    }
  },
  methods: {
    addContact (e) {
      e.preventDefault()
      const newContact = {
        name: this.name,
        email: this.email,
        phone: this.phone,
        isFavorite: this.is_favorite
      }
      this.$emit('add-contact', newContact)

      this.name = ''
      this.email = ''
      this.phone = ''
      this.isFavorite = ''
    }
  }
}
</script>

<style lang="sass" scoped>
    $white: #fff
    $blue: #2874A6
    .form-container
        text-align: left
        background: #efefef
        margin-bottom: 15px
    form
        padding: 15px
        *
            font-size: 16px
        div
            clear: both;
            margin: 10px auto
            label
                float: left
                padding: 5px 0
            label, input
                width: 100%
            input:not(#favorite)
                text-indent: 10px
                height: 35px
                background: $white
                border: none
            &.checkbox-container
                *
                    display: inline
                    width: auto
                    float: none
                input
                    margin-right: 10px
        .submit-container
            text-align: center
            button
                background: $blue
                color: $white
                font-weight: bold
                border: none
                font-size: 16px
                padding: 8px 15px
                border-radius: 4px
                &:hover
                    background: darken($blue, 10%)
</style>
