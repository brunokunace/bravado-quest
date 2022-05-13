<template>
  <div class="search-container">
    <slot name="searchBox" />
    <div class="search-container_content">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchContainer'
}
</script>

<style lang="sass" scoped>
.search-container
  display: flex
  align-items: center
  justify-content: flex-start
  flex-direction: column
  background-color: #fff
  height: 100%
  max-height: 95%
  width: 95%
  max-width: 564px
  padding: 19px 12px 0 12px
  &_content
    margin-top: 20px
    padding-bottom: 20px
    width: 100%
    height: 100%
    max-height: 100%
    overflow-y: auto
</style>
