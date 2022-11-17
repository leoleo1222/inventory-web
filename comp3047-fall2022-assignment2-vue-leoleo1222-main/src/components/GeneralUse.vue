<template>
  <!-- boostrap breadcrumb-->
  <nav aria-label="breadcrumb" v-if="breadcrumb_type || breadcrumb_detail">
    <ol class="breadcrumb">
      <li class="breadcrumb-item">
        <router-link to="/">Home</router-link>
      </li>
      <li class="breadcrumb-item active" aria-current="page" v-if="breadcrumb_detail">
        <router-link :to="'/' + $route.params.type">
          {{
              $route.params.type
          }}
        </router-link>
      </li>
      <li class="breadcrumb-item active" aria-current="page" v-if="!breadcrumb_detail">
        <router-link :to="'/' + $route.params.type">
          {{
              $route.params.type
          }}
        </router-link>
      </li>
      <li class="breadcrumb-item active" aria-current="page" v-if="breadcrumb_detail">
        {{
            $route.params.type
        }}
        detail
      </li>
      <!-- create a boostrap button add align right-->
      <router-link v-if="breadcrumb_type" class="btn btn-primary" aria-current="page" type="button"
        style="margin-left: 80%" :to="'/' + type + '/detail'">
        Add
      </router-link>
    </ol>
  </nav>

  <div v-if="type == 'books' && bookform">
    <!-- boostrap form with six elements-->
    <!-- and two input in a row-->
    <div class="container">
      <form>
        <div class="row">
          <div class="col">
            <!-- input for title-->
            <label for="title" class="form-label">Title</label>
            <input type="text" class="form-control" id="title" placeholder="Title" v-model="inventory.title" />
          </div>
          <div class="col">
            <!-- input for category-->
            <label for="category" class="form-label">Category</label>
            <!-- create a select list for category-->
            <select v-model="inventory.category" class="form-select" aria-label="Default select example">
              <option selected>Open this select menu</option>
              <option value="books">Books</option>
              <option value="games">Games</option>
              <option value="gifts">Gifts</option>
              <option value="materials">Materials</option>
            </select>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for Author-->
            <label for="author" class="form-label">Author</label>
            <input v-model="inventory.author" type="text" class="form-control" id="author" placeholder="Author" />
          </div>
          <div class="col">
            <!-- input for Publisher-->
            <label for="publisher" class="form-label">Publisher</label>
            <input v-model="inventory.publisher" type="text" class="form-control" id="publisher"
              placeholder="Publisher" />
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for year-->
            <label for="year" class="form-label">Year</label>
            <input v-model="inventory.year" type="text" class="form-control" id="year" placeholder="Year" />
          </div>
          <div class="col">
            <!-- input for Location-->
            <label for="location" class="form-label">Location</label>
            <input v-model="inventory.location" type="text" class="form-control" id="location"
              placeholder="Location name in warehouse" />
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for ISBN-->
            <label for="isbn" class="form-label">ISBN</label>
            <input v-model="inventory.isbn" type="text" class="form-control" id="isbn" placeholder="ISBN number" />
          </div>
          <div class="col">
            <!-- input for Image-->
            <label for="image" class="form-label">Image</label>
            <input v-model="inventory.image" type="text" class="form-control" id="image" placeholder="Image URL" />
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for Description with a larger input box-->
            <label for="description" class="form-label">Description</label>
            <textarea v-model="inventory.description" class="form-control" id="description" rows="3"
              placeholder="Description of the item"></textarea>
          </div>
          <div class="col">
            <!-- input for Remark with a larger input box-->
            <label for="remark" class="form-label">Remark</label>
            <textarea v-model="inventory.remark" class="form-control" id="remark" rows="3"
              placeholder="Internal remark"></textarea>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- create a @click button to addInventory()-->
            <button v-if="!route.params.id" class="btn btn-primary me-md-2" type="button" @click="addInventory()">
              Save
            </button>
            <!-- create a @click button to updateInventory()-->
            <div v-if="route.params.id">
              <button class="btn btn-primary me-md-2" type="button" @click="updateInventory()">
                Update
              </button>
            </div>
          </div>
          <div class="col text-end" v-if="route.params.id">
            <!-- create a div align to left-->
            <button class="btn btn-danger" type="button" @click="deleteInventory()">
              Delete
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>

  <div v-if="type == 'games' && gameform">
    <!-- boostrap form with six elements-->
    <!-- and two input in a row-->
    <div class="container">
      <form>
        <div class="row">
          <div class="col">
            <!-- input for title-->
            <label for="title" class="form-label">Title</label>
            <input type="text" class="form-control" id="title" placeholder="Title" v-model="inventory.title" />
          </div>
          <div class="col">
            <!-- input for category-->
            <label for="category" class="form-label">Category</label>
            <!-- create a select list for category-->
            <select v-model="inventory.category" class="form-select" aria-label="Default select example">
              <option selected>Open this select menu</option>
              <option value="books">Books</option>
              <option value="games">Games</option>
              <option value="gifts">Gifts</option>
              <option value="materials">Materials</option>
            </select>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for Image-->
            <label for="image" class="form-label">Image</label>
            <input v-model="inventory.image" type="text" class="form-control" id="image" placeholder="Image URL" />
          </div>
          <div class="col">
            <!-- input for Publisher-->
            <label for="publisher" class="form-label">Publisher</label>
            <input v-model="inventory.publisher" type="text" class="form-control" id="publisher"
              placeholder="Publisher" />
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for quantity-->
            <label for="quantity" class="form-label">Quantity</label>
            <input v-model="inventory.quantity" type="text" class="form-control" id="quantity" placeholder="quantity" />
          </div>
          <div class="col">
            <!-- input for Location-->
            <label for="location" class="form-label">Location</label>
            <input v-model="inventory.location" type="text" class="form-control" id="location"
              placeholder="Location name in warehouse" />
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for Description with a larger input box-->
            <label for="description" class="form-label">Description</label>
            <textarea v-model="inventory.description" class="form-control" id="description" rows="3"
              placeholder="Description show on listing page"></textarea>
          </div>
          <div class="col">
            <!-- input for Remark with a larger input box-->
            <label for="address" class="form-label">Address</label>
            <textarea v-model="inventory.address" class="form-control" id="address" rows="3"
              placeholder="Remarks"></textarea>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- create a @click button to addInventory()-->
            <button v-if="!route.params.id" class="btn btn-primary me-md-2" type="button" @click="addInventory()">
              Save
            </button>
            <!-- create a @click button to updateInventory()-->
            <div v-if="route.params.id">
              <button class="btn btn-primary me-md-2" type="button" @click="updateInventory()">
                Update
              </button>
            </div>
          </div>
          <div class="col text-end">
            <!-- create a div align to left-->
            <button class="btn btn-danger" type="button" @click="deleteInventory()">
              Delete
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>

  <div v-if="type == 'gifts' && giftform">
    <!-- boostrap form with six elements-->
    <!-- and two input in a row-->
    <div class="container">
      <form>
        <div class="row">
          <div class="col">
            <!-- input for title-->
            <label for="title" class="form-label">Title</label>
            <input type="text" class="form-control" id="title" placeholder="Title" v-model="inventory.title" />
          </div>
          <div class="col">
            <!-- input for category-->
            <label for="category" class="form-label">Category</label>
            <!-- create a select list for category-->
            <select v-model="inventory.category" class="form-select" aria-label="Default select example">
              <option selected>Open this select menu</option>
              <option value="books">Books</option>
              <option value="games">Games</option>
              <option value="gifts">Gifts</option>
              <option value="materials">Materials</option>
            </select>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for Image-->
            <label for="image" class="form-label">Image</label>
            <input v-model="inventory.image" type="text" class="form-control" id="image" placeholder="Image URL" />
          </div>
          <div class="col">
            <div class="row">
              <div class="col">
                <!-- input for amount-->
                <label for="amount" class="form-label">Amount</label>
                <input v-model="inventory.amount" type="text" class="form-control" id="amount" placeholder="amount" />
              </div>
              <div class="col">
                <!-- input for unitprice-->
                <label for="unitprice" class="form-label">Unit Price($HKD)</label>
                <input v-model="inventory.unitprice" type="text" class="form-control" id="unitprice"
                  placeholder="unitprice" />
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for donate-->
            <label for="donate" class="form-label">Donated by</label>
            <input v-model="inventory.donate" type="text" class="form-control" id="donate" placeholder="name" />
          </div>
          <div class="col">
            <!-- input for Location-->
            <label for="location" class="form-label">Location</label>
            <input v-model="inventory.location" type="text" class="form-control" id="location"
              placeholder="Location name in warehouse" />
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for Description with a larger input box-->
            <label for="description" class="form-label">Description</label>
            <textarea v-model="inventory.description" class="form-control" id="description" rows="3"
              placeholder="Description show on listing page"></textarea>
          </div>
          <div class="col">
            <!-- input for Remark with a larger input box-->
            <label for="address" class="form-label">Address</label>
            <textarea v-model="inventory.address" class="form-control" id="address" rows="3"
              placeholder="Remarks"></textarea>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- create a @click button to addInventory()-->
            <button v-if="!route.params.id" class="btn btn-primary me-md-2" type="button" @click="addInventory()">
              Save
            </button>
            <!-- create a @click button to updateInventory()-->
            <div v-if="route.params.id">
              <button class="btn btn-primary me-md-2" type="button" @click="updateInventory()">
                Update
              </button>
            </div>
          </div>
          <div class="col text-end">
            <!-- create a div align to left-->
            <button class="btn btn-danger" type="button" @click="deleteInventory()">
              Delete
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>

  <div v-if="type == 'material' && materialform">
    <!-- boostrap form with six elements-->
    <!-- and two input in a row-->
    <div class="container">
      <form>
        <div class="row">
          <div class="col">
            <!-- input for title-->
            <label for="title" class="form-label">Title</label>
            <input type="text" class="form-control" id="title" placeholder="Title" v-model="inventory.title" />
          </div>
          <div class="col">
            <!-- input for category-->
            <label for="category" class="form-label">Category</label>
            <!-- create a select list for category-->
            <select v-model="inventory.category" class="form-select" aria-label="Default select example">
              <option selected>Open this select menu</option>
              <option value="books">Books</option>
              <option value="games">Games</option>
              <option value="gifts">Gifts</option>
              <option value="material">Materials</option>
            </select>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for Image-->
            <label for="image" class="form-label">Image</label>
            <input v-model="inventory.image" type="text" class="form-control" id="image" placeholder="Image URL" />
          </div>
          <div class="col">
            <div class="row">
              <div class="col">
                <!-- input for quantity-->
                <label for="quantity" class="form-label">Quantity</label>
                <input v-model="inventory.amount" type="text" class="form-control" id="quantity"
                  placeholder="quantity" />
              </div>
              <div class="col">
                <!-- input for location-->
                <label for="location" class="form-label">Location</label>
                <input v-model="inventory.location" type="text" class="form-control" id="location"
                  placeholder="location in warehouse" />
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- input for Description with a larger input box-->
            <label for="description" class="form-label">Description</label>
            <textarea v-model="inventory.description" class="form-control" id="description" rows="3"
              placeholder="Description show on listing page"></textarea>
          </div>
          <div class="col">
            <!-- input for Remark with a larger input box-->
            <label for="address" class="form-label">Address</label>
            <textarea v-model="inventory.address" class="form-control" id="address" rows="3"
              placeholder="Remarks"></textarea>
          </div>
        </div>
        <div class="row">
          <div class="col">
            <!-- create a @click button to addInventory()-->
            <button v-if="!route.params.id" class="btn btn-primary me-md-2" type="button" @click="addInventory()">
              Save
            </button>
            <!-- create a @click button to updateInventory()-->
            <div v-if="route.params.id">
              <button class="btn btn-primary me-md-2" type="button" @click="updateInventory()">
                Update
              </button>
            </div>
          </div>
          <div class="col text-end">
            <!-- create a div align to left-->
            <button class="btn btn-danger" type="button" @click="deleteInventory()">
              Delete
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { useRoute } from "vue-router";
import { ref, onMounted, computed } from "vue";

export default {
  name: "GeneralUse",
  props: {
    type: String,
    navbar: Boolean,
    bookform: Boolean,
    gameform: Boolean,
    giftform: Boolean,
    materialform: Boolean,
    breadcrumb_type: Boolean,
    breadcrumb_detail: Boolean,
    typecards: Boolean,
  },
  setup(props) {
    const route = useRoute();
    // define the inventory object
    const inventory = ref({});
    const add_inventory = ref({});
    const lastPage = ref(0);

    onMounted(async () => {
      if (route.params.id) {
        const response = await fetch(`/api/${props.type}/${route.params.id}`);
        inventory.value = await response.json();
      }
    });

    // createa Instance method to update the form data to the inventory object
    const updateInventory = () => {
      // console.log(inventory.value);
      // console.log(route.params.id);
      fetch(`/api/${props.type}/${route.params.id}`, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(inventory.value),
      })
        .then((res) => res.json())
        .then((data) => {
          console.log(data);
          alert(data);
        });
    };

    // createa Instance method to delete the form data to the inventory object
    const deleteInventory = async () => {
      // console.log(inventory.value);
      // console.log(route.params.id);
      var response = await fetch(`/api/${props.type}/${route.params.id}`, {
        method: "DELETE",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(inventory.value),
      });
      if (response.ok) {
        var text = await response.json();
        alert(text);
        location.assign(`/${props.type}`);
      } else {
        alert(response.statusText);
      }
      // fetch(`/api/${props.type}/${route.params.id}`, {
      //   method: "DELETE",
      //   headers: {
      //     "Content-Type": "application/json",
      //   },
      //   body: JSON.stringify(inventory.value),
      // })
      //   .then((res) => res.json())
      //   .then((data) => {
      //     console.log(data);
      //     alert(data);
      //     location.assign(`/${props.type}`)

      //   });
    };

    // createa Instance method to add the form data to the inventory object
    const addInventory = async () => {
      // alert("in add inventory");

      var response = await fetch("/api/inventory/", {
        method: "post",
        headers: {
          "Content-Type": "application/json",
        },

        body: JSON.stringify(inventory.value),
      });

      alert(response.statusText);
    };

    const pages = computed(function () {
      var pages = [];

      for (var i = 1; i <= lastPage.value; i++) {
        pages.push(i);
      }

      return pages;
    });

    return {
      addInventory,
      route,
      inventory,
      add_inventory,
      pages,
      updateInventory,
      deleteInventory,
    };
  },
};
</script>
