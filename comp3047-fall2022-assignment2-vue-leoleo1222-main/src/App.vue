<template>
  <!-- boostrap navbar-->
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
      <router-link class="nav-link active" aria-current="page" :to="'/'">
        <a class="navbar-brand" href="#">Inventory</a>
      </router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/books">
              Books
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/games">
              Games
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/gifts">
              Gifts
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/material">
              Material
            </router-link>
          </li>
        </ul>
        <form class="d-flex" role="search">
          <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search"
            v-model="search_title" />
          <!-- router link to search page-->
          <button class="btn btn-outline-success" aria-current="page" type="button" @click="search">
            Search
          </button>
        </form>
      </div>
    </div>
  </nav>
  <div class="container text-start">
    <router-view />
  </div>
</template>

<script>
import { ref } from "vue";
import { useRouter } from "vue-router";

export default {
  name: "App",
  setup() {
    const search_title = ref("");
    const router = useRouter();


    const search = async () => {

      alert("search");

      router.push({
        name: 'search',
        query: {
          title: search_title.value
        },
      })
    };




    return {
      search_title,
      search,

    };
  },
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
