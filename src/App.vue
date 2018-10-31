<template>
  <div id="app">
    <p>{{ info }} </p>
    <button :disabled="disabled" @click="onAction">With Delay</button>
  </div>
</template>

<script>
import debounce from 'lodash/debounce';

const DELAY_TIME = 1000;

export default {
  name: 'app',
  data() {
    return {
      disabled: false,
      delay: null,
      info: '',
      time: {
        start: null,
        end: null,
      },
    }
  },
  created() {
    this.withDelay = debounce(() => {
      this.something();
      this.disabled = false;
    }, DELAY_TIME);
  },
  methods: {
    something() {
      // faz alguma coisa
      this.time = { ...this.time, end: new Date().getTime() };
      this.info = `execution time: ${this.time.end}`;
      console.log(this.info);
      console.log(`delayed time: ${this.time.end - this.time.start}`);
      console.log('===============================');
    },
    onAction() {
      this.time = { ...this.time, start: new Date().getTime() };
      console.log('===============================');
      this.info = `start callback with delay in: ${this.time.start}`;
      console.log(this.info);
      this.disabled = true;
      this.withDelay();
    },
  },
}
</script>
