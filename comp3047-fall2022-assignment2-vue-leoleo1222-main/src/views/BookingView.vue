<template>
  <div class="home">
    <div class="container">
      <ul class="list-group">
        <li class="list-group-item">{{ booking._id }}</li>
        <li class="list-group-item">{{ booking.email }}</li>
        <li class="list-group-item">A third item</li>
        <li class="list-group-item">A fourth item</li>
        <li class="list-group-item">And a fifth one</li>
      </ul>
    </div>
  </div>
  <!-- <PaginatedBookings /> -->
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
// import PaginatedBookings from '@/components/PaginatedBookings.vue'
import { useRoute } from "vue-router";
import { ref, onMounted } from "vue";

export default {
  name: 'HomeView',
  components: {
    // HelloWorld
    // PaginatedBookings
  },
  setup() {
    const booking = ref({});
    const route = useRoute();

    onMounted(async () => {

      var response = await fetch("/api/bookings/" + route.params.id);

      if (response.ok) {
        booking.value = await response.json();
      } else {
        alert(response.statusText);
      }
    })

    return {
      booking
    }
  }
}
</script>
