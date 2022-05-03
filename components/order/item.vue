<template>
  <a :href="`/orders/${order.id}`" class="flex flex-col border-b-2 border-gray-400 py-2">
    <div class="flex justify-between p-2">
      <h5 class="text-md font-semibold text-gray-700">{{ order.trip.name }}</h5>

      <div v-if="order.mostUrgentTodo && order.mostUrgentTodo.dueDate" class="flex items-center px-2 py-1 text-gray-600 bg-gray-200 border border-gray-400">
        <div class="rounded-full p-2 bg-red-500 mr-2"></div>
        <time :datetime="order.mostUrgentTodo.dueDate">{{ order.mostUrgentTodo.dueDate }}</time>
      </div>
    </div>
    <div class="flex flex-row m-2 items-center">
      <badge>
        <div class="flex flex-row items-center">
          <div class="pr-2" style="height: 15px; width: 23px">
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M147.8 192H480V144C480 117.5 458.5 96 432 96h-160l-64-64h-160C21.49 32 0 53.49 0 80v328.4l90.54-181.1C101.4 205.6 123.4 192 147.8 192zM543.1 224H147.8C135.7 224 124.6 230.8 119.2 241.7L0 480h447.1c12.12 0 23.2-6.852 28.62-17.69l96-192C583.2 249 567.7 224 543.1 224z"/></svg>
          </div>
          {{ order.id }}
        </div>
      </badge>
      <badge primary>{{ order.client.shortName }}</badge>
      <badge primary>{{ order.trip.destinations.map(d => d.name).join(', ') }}</badge>
      <avatar class="ml-auto" :user="order.user" />
    </div>
  </a>
</template>

<script>
export default {
  name: "OrderItem",
  props: {
    order: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
</style>