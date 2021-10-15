<template>
  <b-card :sub-title="`Result #${number}`" class="mb-2">
    {{ content }}
  </b-card>
</template>

<script>
export default {
  name: 'ResultCard',

  props: {
    number: Number,
    content: undefined
  }
}
</script>
