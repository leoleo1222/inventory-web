<template>
  asdasdsad
  <GeneralUse :type="$route.params.type" navbar="true" breadcrumb_type="true" />
  <div>
    <!-- {{ $route.params.type }} -->
    <!-- boostrap create six card and three cards in a row-->
    <div class="container">
      <div class="row row-cols-1 row-cols-md-3 g-4">
        <div class="col" v-for="item in inventory" :key="item._id">
          <div class="card">
            <!-- router link the image to /:type/detail/:id/ and bring the item._id-->
            <router-link :to="'/' + $route.params.type + '/detail/' + item._id">
              <img :src="item.image" class="card-img-top" alt="..." />
            </router-link>
            <div class="card-body">
              <h5 class="card-title">{{ item.title }}</h5>
              <p class="card-text">{{ item.image }}</p>
              <!-- <router-link :to="`/inventory/${item._id}`" class="btn btn-primary">Details</router-link> -->
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- boostrap pagination button with 3 page selection next prev in center-->
    <nav aria-label="Page navigation example">
      <ul class="pagination justify-content-center">
        <button class="page-link" @click="fetchPage(currentPage - 1, $route.params.type)"
          :disabled="currentPage < 2">Pre</button>
        <!-- three pagination button in a v for-->
        <li class="page-item" v-for="i in pages" :key="i">
          <button class="page-link" @click="fetchPage(i, $route.params.type)">{{ i }}</button>
        </li>
        <button class="page-link" @click="fetchPage( currentPage + 4, $route.params.type)"
          :disabled="currentPage > lastPage - 1">Next</button>
      </ul>
    </nav>
  </div>
</template>


<script>
import { useRoute } from "vue-router";
import { ref, onMounted, computed, watch } from "vue";
import GeneralUse from "@/components/GeneralUse.vue";
// import { watch } from "fs";

export default {
  name: "SearchView",
  components: {
    GeneralUse,
  },
  props: {
    type: String,
    navbar: Boolean,
    bookform: Boolean,
    breadcrumb_type: Boolean,
    breadcrumb_detail: Boolean,
    typecards: Boolean,
  },
  setup() {
    const route = useRoute();
    // define the inventory object
    const inventory = ref({});
    const add_inventory = ref({});
    const lastPage = ref(0);
    const perPage = ref(6);
    const currentPage = ref(1);
    // const title = ref(useRoute().query.title);


    // const type = ref(props.type);

    const pages = computed(function () {
      var pages = [];

      for (var i = Math.max(1, currentPage.value); i <= Math.min(currentPage.value + 2, lastPage.value); i++) {
        pages.push(i)
      }

      return pages;
    });

    const fetchPage = async function (page) {

      currentPage.value = page;

      var response = await fetch("/api/inventory?perPage=" + perPage.value + "&page=" + page + "&title=" + route.query.title);

      if (response.ok) {
        var data = await response.json();

        inventory.value = data.inventory;
        lastPage.value = data.pages

      } else {
        alert(response.statusText);
      }
    };

    // onUpdated(async () => {
    //   await fetchPage(1);
    // });

    onMounted(async () => {
      await fetchPage(currentPage.value);
    });

    watch(() => route.query.title, () => fetchPage(currentPage.value));

    return {
      fetchPage,
      route,
      inventory,
      add_inventory,
      pages,
      currentPage,
      lastPage,
    };
  },
};
</script>

