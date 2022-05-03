<template>
  <div class="px-2 py-2 rounded-full bg-green-800 text-sm text-white font-bold">
    {{user.firstName[0]}}{{user.lastName[0]}}
  </div>
</template>

<script>
export default {
  name: "Avatar",
  props: {
    user: {
      type: Object,
      required: true
    }
  }
}
</script>