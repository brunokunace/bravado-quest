<template>
  <div class="page">
    <search-container>
      <template #searchBox>
        <search-input v-model="filter" />
      </template>
      <recycle-scroller
        v-slot="{ item }"
        class="scroller"
        :items="userList"
        :item-size="160"
        key-field="email"
      >
        <user-card
          v-bind="item"
          :key="item.email"
          :filter="filter"
          @selected="selectUser"
        />
      </recycle-scroller>
    </search-container>
  </div>
</template>

<script>
import users from '~/static/users.json'
export default {
  name: 'IndexPage',
  data: () => ({
    filter: '',
    users: []
  }),
  computed: {
    userList () {
      const filter = this.filter.toLocaleLowerCase()
      const fields = ['name', 'email', 'title', 'address']
      return this.users.filter((user) => {
        return fields.some(field => user[field].toLowerCase().includes(filter))
      })
    }
  },
  mounted () {
    this.users = users.map((user) => {
      return { ...user, selected: false, address: `${user.address}, ${user.city}` }
    })
  },
  methods: {
    selectUser (payload) {
      const index = this.users.findIndex(user => user.email === payload.email)
      this.users[index].selected = payload.selected
    }
  }
}
</script>
<style lang="sass" scoped>
.page
  display: flex
  width: 100vw
  height: 100vh
  align-items: center
  justify-content: center
.scroller
  height: 100%
</style>
