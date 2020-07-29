<style scoped>
.addmargin {
  margin-top: 10px;
  margin-bottom: 10px;
}

.vue-logo-back {
  background-color: #8bba87;
  height: 3rem;
  color: white;
  font-size: xx-large;
}
.col-md-6 {
  display: flex;
  margin-top: 3rem;
  max-width: 60%;
}
.card {
  margin-right: 2rem;
  width: 18rem;
}
</style>

<template>
  <div class="home">
    <div class="vue-logo-back">
      <div>List of customer</div>
    </div>
    <div class="col-md-6 centeralign">
      <div
        class="card centeralign addmargin"
        v-for="customer in customerlist"
        :key="customer.id"
      >
        <div class="card-body" v-on:click="setSelectedCustomer(customer.name)">
          <h5 class="card-title">{{ customer.name }}</h5>
          <p class="card-text">{{ customer.email }}</p>
          <p class="card-text">{{ customer.phone }}</p>

          <a class="btn btn-primary" v-on:click="goToDetailsPage(customer.id)"
            ><span style="color: white;">Click for more details</span></a
          >
        </div>
      </div>
    </div>
    <Display
      v-if="selectedCustomer != ''"
      :selectedCustomer="selectedCustomer"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import Display from "@/components/Display.vue";
import axios from "axios";

export default {
  name: "customers",
  mounted() {
    axios({
      method: "GET",
      url: "assets/samplejson/customerlist.json",
    }).then(
      (response) => {
        this.customerlist = response.data;
      },
      (error) => {
        // eslint-disable-next-line
        console.error(error);
      }
    );
  },
  data() {
    return {
      customerlist: [],
      selectedCustomer: "",
    };
  },
  components: {
    Display,
  },
  methods: {
    setSelectedCustomer: function (name) {
      this.selectedCustomer = name;
    },
    goToDetailsPage: function (id) {
      this.$router.push("/customerdetails/" + id);
    },
  },
};
</script>
