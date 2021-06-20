<template>
  <div>
    <h1>Event listing</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>
<script>
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService.js'

export default {
  components: { EventCard },
  data() {
    return {
      events: [],
    }
  },
  created() {
    EventService.getEvents('http://localhost:3000/events')
      .then((response) => {
        response.data.forEach((element) => {
          this.events.push(element)
        })
      })
      .catch((error) => {
        console.error(error)
      })
  },
}
</script>
