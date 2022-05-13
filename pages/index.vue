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
export default {
  name: 'IndexPage',
  async asyncData ({ $axios }) {
    const usersUrl = 'https://gist.githubusercontent.com/allaud/093aa499998b7843bb10b44ea6ea02dc/raw/c400744999bf4b308f67807729a6635ced0c8644/users.json'
    const users = await $axios.$get(usersUrl)
    users.map((user) => {
      return { ...user, selected: false, address: `${user.address}, ${user.city}` }
    })
    return { users }
  },
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
