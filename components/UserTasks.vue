<template>
  <div>
    <div class="mb-3">
      <Avatar
        :url="user.avatar"
      />
      {{ user.name }}
    </div>

    <Tasks
      @change-page="changePage($event)"
    />
  </div>
</template>

<script>
import Tasks from '~/components/Tasks'
import Avatar from '~/components/Avatar'

export default {
  components: { Avatar, Tasks },

  computed: {
    user() {
      return this.$store.state.user
    },
  },

  async created() {
    this.$store.dispatch('user/fetch', this.$route.params.id)
    this.$store.dispatch('tasks/fetchUser', {
      page: 1,
      id: this.$route.params.id,
    })
  },

  methods: {
    async changePage(page) {
      await this.$store.dispatch('tasks/fetchUser', {
        page: page,
        id: this.$route.params.id,
      })
    },
  },
}
</script>

<style scoped>
</style>
