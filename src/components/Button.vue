<template>
  <button class="btn" @click="$emit('btn-click')">
    {{text}}
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    text: String,
  }
}
</script>