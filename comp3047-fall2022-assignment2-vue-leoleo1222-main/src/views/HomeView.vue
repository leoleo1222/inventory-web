<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->

    <!-- <PaginatedGift v-if="booking.type=='gift'" msg="Welcome to Your Vue.js App" />
    <PaginatedBookings msg="Welcome to Your Vue.js App" />
    <PaginatedBookings msg="Welcome to Your Vue.js App" />
    <PaginatedBookings msg="Welcome to Your Vue.js App" /> -->
  </div>

  <!-- Use the component GeneralUse-->
  <nav aria-label="breadcrumb" v-if="breadcrumb_type || breadcrumb_detail">
    <ol class="breadcrumb">
      <li class="breadcrumb-item">
        <router-link to="/">Home</router-link>
      </li>
    </ol>
  </nav>

  <div class="container my-5">
    <div class="card-group">
      <div class="card">
        <div class="card-body">
          <div class="jumbotron jumbotron-fluid">
            <div class="container">
              <h1 class="display-4">Inventory System</h1>
              <p class="lead">
                This is a modified jumbotron that occupies the entire horizontal
                space of its parent.
              </p>
            </div>
          </div>
        </div>
      </div>
      <div class="card">
        <div class="card-body">
          <apexchart width="580" type="pie" :options="options" :series="series"></apexchart>
        </div>
      </div>
    </div>
  </div>


  <div class="card-group">
    <div class="card text-center" style="width: 18rem">
      <router-link :to="'/books'">
        <img src="https://openclipart.org/image/800px/svg_to_png/275692/1489798288.png" class="card-img-top" alt="" />
      </router-link>
      <div class="card-body">
        <h5 class="card-title">Books</h5>
      </div>
    </div>

    <div class="card text-center">
      <router-link :to="'/games'">
        <img src="https://th.bing.com/th/id/OIP.yBUPi-O0m7PEslfN4PvkNQHaHa?pid=ImgDet&rs=1" class="card-img-top" alt="" />
      </router-link>
      <div class="card-body">
        <h5 class="card-title">Games</h5>
      </div>
    </div>

    <div class="card text-center">
      <router-link :to="'/gifts'">
        <img src="https://th.bing.com/th/id/R.7a9fcb9a4c22dc97c2dab447728c3886?rik=pSz4GEHpHszHsA&pid=ImgRaw&r=0" class="card-img-top" alt="" />
      </router-link>
      <div class="card-body">
        <h5 class="card-title">Gifts</h5>
      </div>
    </div>

    <div class="card text-center">
      <router-link :to="'/materials'">
        <img src="https://cdn4.iconfinder.com/data/icons/STROKE/project_managment/png/400/materials.png" class="card-img-top" alt="" />
      </router-link>
      <div class="card-body">
        <h5 class="card-title">Materials</h5>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import { ref, onMounted } from "vue";

export default {
  name: 'HomeView',
  components: {

  },
  setup() {
    const options = ref({
      chart: {
        width: 380,
        type: 'pie',
      },
      colors: ['#93C3EE', '#E5C6A0', '#669DB5', '#94A74A'],
      fill: {
        type: 'image',
        opacity: 0.85,
        image: {
          src: ['https://openclipart.org/image/800px/svg_to_png/275692/1489798288.png', 'https://th.bing.com/th/id/OIP.yBUPi-O0m7PEslfN4PvkNQHaHa?pid=ImgDet&rs=1'
          , 'https://th.bing.com/th/id/R.7a9fcb9a4c22dc97c2dab447728c3886?rik=pSz4GEHpHszHsA&pid=ImgRaw&r=0'
          , 'https://cdn4.iconfinder.com/data/icons/STROKE/project_managment/png/400/materials.png'],
          width: 25,
          imagedHeight: 25
        },
      },
      stroke: {
        width: 4
      },
      dataLabels: {
        enabled: true,
        style: {
          colors: ['#111']
        },
        background: {
          enabled: true,
          foreColor: '#fff',
          borderWidth: 0
        }
      },
      responsive: [{
        breakpoint: 480,
        options: {
          chart: {
            width: 200
          },
          legend: {
            position: 'bottom'
          }
        }
      }]
    },);
    const series = ref([]);

    onMounted(async () => {

      var response = await fetch("/api/inventory/aggregate/groupby");

      if (response.ok) {
        var heroes = await response.json();

        // alert(JSON.stringify(heroes));

        series.value = heroes.map(a => a.count);
        options.value = { ... { labels: heroes.map(a => a._id) } };
      }
    });
    return {
      options, series
    }
  }
}
</script>
