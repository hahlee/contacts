<template>
    <div class="contact-list">
        <ul>
            <li class="item" v-for="contact in contacts" :key="contact.id" :id="contact.id">
                <ContactItem v-bind:contact="contact"/>
                <!-- <ContactItem v-bind:contact="contact" v-on:del-contact="$emit('del-contact', contact.id)"/> -->
            </li>
        </ul>
    </div>
</template>

<script>
import ContactItem from '@/components/ContactItem'

export default {
  name: 'Contacts',
  components: {
    ContactItem
  },
  props: ['contacts']
}
</script>

<style lang="sass" scoped>
    $alignLeft: left
    $gray: #efefef
    $grayBlue: #eaf1f8
    $width90: 90%
    $zeroMargin: 0 auto
    $listPadding: 25px
    .contact-list
        border: 1px solid $gray
        text-align: $alignLeft
        ul
            list-style-type: none
            padding: 0
            margin: $zeroMargin
            .item
                padding: $listPadding
                &:nth-child(odd)
                    background-color: $grayBlue
                &:hover
                    p.contact-name
                        text-decoration: underline
</style>
