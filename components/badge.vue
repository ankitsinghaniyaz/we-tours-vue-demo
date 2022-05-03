<template>
  <div 
    class="text-sm py-1 px-2 border border-gray-300 rounded mr-4 truncate bg-white"
    :class="{'bg-primary': primary, 'text-white': primary}"
    style="max-width: 200px"
  >
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Badge",
  props: {
    primary: {
      type: Boolean,
      default: false,
    },
  },
}
</script>