<template>
  <main class="bg-gray-300 min-h-screen h-full border-t-8 border-primary">
    <header class="flex items-center justify-between p-4">
      <h1 class="font-semibold text-lg">Orders</h1>
      <avatar v-if="filters.user" :user="filter.user" />
    </header>

    <section class="flex flex-row items-center px-4 py-2 border-t-2 border-gray-400">
      <div class="h-4 w-4 mr-4">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M3.853 54.87C10.47 40.9 24.54 32 40 32H472C487.5 32 501.5 40.9 508.1 54.87C514.8 68.84 512.7 85.37 502.1 97.33L320 320.9V448C320 460.1 313.2 471.2 302.3 476.6C291.5 482 278.5 480.9 268.8 473.6L204.8 425.6C196.7 419.6 192 410.1 192 400V320.9L9.042 97.33C-.745 85.37-2.765 68.84 3.854 54.87L3.853 54.87z"/></svg>
      </div>
      <input v-model="filters.search" @input="applyFilter" class="w-full p-2 placeholder:text-slate-400 rounded" placeholder="Search for orders" />
    </section>

    <section class="flex flex-row items-center p-4 bg-gray-200 justify-between">
      <div>
        Orders in the next &nbsp;&nbsp;
        <select class="px-1 py-2 bg-white" v-model="filters.days">
          <option value="7 days">7 days</option>
          <option value="30 days">30 days</option>
          <option value="180 days">180 days</option>
        </select>
      </div>
      <div class="bg-white px-1 py-2 rounded-full text-sm text-gray-500">
        {{ orders.length }}
      </div>
    </section>

    <loader height="100px" v-if="fetchingOrders" />
    <section v-else>
      <order-item
        :order="order"
        v-for="order of orders"
        id="`order-${order.id}`"
        :key="`order-${order.id}`"
      >
      </order-item>
    </section>
  </main>
</template>

<script>
import axios from "axios";
import throttle from "lodash/throttle";

export default {
  name: "Orders",
  data() {
    return {
      filters: {
        search: "",
        days: "7 days",
      },
      orders: [],
      fetchingOrders: false,
    };
  },
  methods: {
    applyFilter() {
      this.fetchOrdersThrottled();
    },
    fetchOrdersThrottled: throttle(function(vm) { 
      this.fetchOrders()
    }, 2500),
    async fetchOrders() {
      this.fetchingOrders = true;
      try {
        const { data: orders } = await axios.get(
          "https://demo-travelize.buspaket.de/api/public/orders",
          {
            params: {
              '_search': this.filters.search,
            },
          }
        );
        this.orders = orders;
      } finally {
        this.fetchingOrders = false;
      }
    },
  },
  mounted() {
    this.fetchOrders();
  },
};
</script>

<style>
</style>
