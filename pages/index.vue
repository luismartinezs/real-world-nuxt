<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="(event, index) in events" :key="index" :event="event" />
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get('http://localhost:3000/events')
      return {
        events: data,
      }
    } catch (_) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time, please try later',
      })
    }
  },
  head() {
    return {
      title: 'Event listing',
    }
  },
}
</script>
