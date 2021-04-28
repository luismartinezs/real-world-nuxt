<template>
  <div>
    <h1>{{ event.title }}</h1>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, error, params }) {
    try {
      const { data } = await $axios.get(
        'http://localhost:3000/events/' + params.id
      )
      return {
        event: data,
      }
    } catch (_) {
      error({
        statusCode: 503,
        message: `Unable to fetch event # ${params.id} at this time, please try later`,
      })
    }
  },
  head() {
    return {
      title: `Event ${this.event.title}`,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: `What you need to know about event ${this.event.title}`,
        },
      ],
    }
  },
  computed: {
    id() {
      return this.$route.params.id
    },
  },
}
</script>
