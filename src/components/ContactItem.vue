<template>
    <div v-bind:class="{'favorite': contact.is_favorite}">
        <div>
            <div class="favorite-btn">
                <label>
                    <input type="checkbox" v-on:change="markFavorite">
                    <span>&hearts;</span>
                </label>
            </div>
            <p class="contact-name inline">{{contact.name}}</p>
            <div class="inline float-right">
                <small class="inline show-details" @click="toggleDetails()" :class="[ isVisible ? 'open' : 'closed' ]"></small>
                <button class="del" @click="$emit('del-contact', contact.id)">DELETE</button>
            </div>
            <div class="contact-details" :class="[ isVisible ? 'show' : 'hide' ]">
                <ul>
                    <li>Email: {{contact.email}}</li>
                    <li>Phone: {{contact.phone}}</li>
                    <li>Favorite Contact: {{contact.is_favorite}}</li>
                    <li>ID: {{contact.id}}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ContactItem',
  props: ['contact'],
  data () {
    return {
      isVisible: false
    }
  },
  methods: {
    markFavorite () {
      this.contact.is_favorite = !this.contact.is_favorite
    },
    toggleDetails () {
      this.isVisible = !this.isVisible
    }
  }
}
</script>

<style lang="sass" scoped>
    .item
        &:hover
            p.contact-name
                text-decoration: underline
    div
        .favorite-btn
            color: grey
            overflow: auto
            float: left
            position: relative
            margin-right: 10px
            label
                float: left
                span
                    text-align: center
                    display: block
                    font-size: 24px
                    position: relative
                    top: -6px
                input
                    display: none
        &.favorite
            p
                font-weight: bold
            .favorite-btn
                color: red
        .inline
            display: inline
        .float-right
            float: right
        .del
            display: none
            color: #fff
            border-radius: 4px
            border: none
            background: red
            margin-left: 10px
        .show-details
            font-size: x-small
            text-transform: uppercase
            &.open
                &:after
                    content: "Hide Details \25B2"
            &.closed
                &:after
                    content: "Show Details \25BC"
        .contact-details
            ul
                list-style-type: none
                font-weight: normal
                padding: 20px
            &.show
                display: block
            &.hide
                display: none
</style>
