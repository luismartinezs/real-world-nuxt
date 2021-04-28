<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="(event, index) in events" :key="index" :event="event" />
  </div>
</template>

<script>
export default {
  asyncData({ $axios, error }) {
    return $axios
      .get('http://localhost:3000/events')
      .then((res) => {
        return {
          events: res.data,
        }
      })
      .catch(() => {
        error({
          statusCode: 503,
          message: 'Unable to fetch events at this time, please try later',
        })
      })
  },
  head() {
    return {
      title: 'Event listing',
    }
  },
}
</script>
