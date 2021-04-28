<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="(event, index) in events" :key="index" :event="event" />
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
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
  computed: mapState({
    events: (state) => state.events.events,
  }),
}
</script>
