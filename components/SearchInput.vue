<template>
  <div class="search-input">
    <slot name="prepend">
      <div class="search-input_prepend">
        <fa :icon="prependIcon" :color="prependIconColor" class="search-input_prepend-icon" />
      </div>
    </slot>
    <input type="text" class="search-input_input" :value="value" @input="inputHandler($event.target.value)">
    <slot name="postpend" />
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    prependIcon: {
      type: String,
      default: 'magnifying-glass'
    },
    prependIconColor: {
      type: String,
      default: '#737373'
    }
  },
  data: () => ({
    value: ''
  }),
  mounted () {
    this.value = this.$route.path.substring(1)
    this.inputHandler(this.value)
  },
  methods: {
    inputHandler (value) {
      this.$emit('input', value)
    }
  }
}
</script>

<style lang="sass" scoped>
.search-input
  display: flex
  flex-direction: row
  width: 100%
  height: 48px
  min-height: 48px
  background: #FAFAFA
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.12), 0 2px 2px rgba(0, 0, 0, 0.24)
  border-radius: 2px
  &_input
    width: 100%
    border: none
    font-size: 24px
    line-height: 28px
    color: rgba(0, 0, 0, 0.75)
    background-color: transparent
    &:focus
      outline: none
  &_prepend
    display: flex
    align-items: center
    justify-content: center
    width: 50px
    height: 100%
    &-icon
      width: 18px
      height: 18px
</style>
