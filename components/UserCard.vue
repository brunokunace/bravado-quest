<template>
  <div class="user-card" :class="{ active: selected }">
    <div class="user-card_avatar">
      <img :src="avatar" alt="avatar">
    </div>
    <div class="user-card_content">
      <div class="user-card_content_info">
        <div class="user-card_content_info_name-wrapper">
          <p class="user-card_content_info_name" v-html="highlightText(name)" />
          <p class="user-card_content_info_email" v-html="highlightText(email)" />
        </div>
        <p class="user-card_content_info_title" v-html="highlightText(title)" />
        <p class="user-card_content_info_address" v-html="highlightText(address)" />
      </div>
      <div class="user-card_action">
        <p class="user-card_action-text" @click="actionHandler">
          {{ actionText }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserCard',
  props: {
    avatar: {
      type: String,
      default: ''
    },
    name: {
      type: String,
      default: ''
    },
    email: {
      type: String,
      default: ''
    },
    title: {
      type: String,
      default: ''
    },
    address: {
      type: String,
      default: ''
    },
    selected: {
      type: Boolean,
      default: false
    },
    filter: {
      type: String,
      default: ''
    }
  },
  computed: {
    actionText () {
      return this.selected ? 'SKIP SELECTION' : 'MARK AS SIUTABLE'
    }
  },
  methods: {
    actionHandler () {
      this.$emit('selected', { email: this.email, selected: !this.selected })
    },
    highlightText (text) {
      return text.replaceAll(this.filter, `<mark>${this.filter}</mark>`)
    }
  }
}
</script>

<style lang="sass" scoped>
$mobileWidth: 480px
.user-card
  display: flex
  align-items: center
  justify-content: center
  flex-direction: row
  background: #FAFAFA
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.12), 0 2px 2px rgba(0, 0, 0, 0.24)
  border-radius: 3px
  height: 136px
  width: 100%
  border: 1px solid transparent
  &.active
    border-color: #4765FF
  &_avatar
    display: flex
    width: 100%
    height: 100%
    max-width: 136px
    max-height: 136px
    min-width: 136px
    min-height: 135px
    background-color: #BCBCBC
    border-top-left-radius: 3px
    border-bottom-left-radius: 3px
    img
      width: 100%
      min-width: 136px
      border-top-left-radius: 3px
      border-bottom-left-radius: 3px
  &_content
    width: 100%
    height: 100%
    display: flex
    flex-direction: column
    &_info
      display: flex
      flex-direction: column
      padding: 10px 10px 5px 27.5px
      border-bottom: 1px solid rgba(0, 0, 0, 0.12)
      &_name-wrapper
        display: flex
        flex-direction: row
        justify-content: space-between
        align-items: flex-start
        flex-wrap: wrap
      &_name
        font-size: 24px
        line-height: 32px
        @media (max-width: $mobileWidth)
          font-size: 16px
          line-height: 20px
      &_email
        font-size: 14px
        line-height: 16px
        color: rgba(0, 0, 0, 0.5)
        @media (max-width: $mobileWidth)
          font-size: 12px
          line-height: 14px
      &_title
        font-weight: 700
        font-size: 14px
        line-height: 20px
        color: rgba(0, 0, 0, 0.5)
        @media (max-width: $mobileWidth)
          font-size: 12px
          line-height: 14px
      &_address
        font-size: 14px
        line-height: 20px
        color: rgba(0, 0, 0, 0.5)
        @media (max-width: $mobileWidth)
          font-size: 12px
          line-height: 14px
  &_action
    display: flex
    align-items: center
    justify-content: flex-start
    padding-left: 32px
    width: 100%
    height: 100%
    &-text
      color: #009688
      font-weight: 500
      font-size: 14px
      line-height: 16px
      cursor: pointer
</style>
