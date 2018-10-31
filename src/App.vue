<template>
  <div id="app">
    <button @click="delay">delay</button>
  </div>
</template>

<script>
import debounce from 'lodash/debounce';

export default {
  name: 'app',
  data() {
    return {
      delay: null,
    }
  },
  created() {
    this.delay = debounce(() => this.print(), 500);
  },
  methods: {
    print() {
      console.log('disparou de dentro do debounce')
    },
  },
}
</script>
