<template>
  <div>
    <p>{{ time }}</p>
    <button @click="run">{{ stage }}</button>
    <button @click="stop">Stop</button>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'home',
  data() {
    return {
      startTime: 0,
      interval: null,
      pauseDiff: 0,
      diff: 0,
      stage: 'Start',
    };
  },
  mounted() {
    if (localStorage.getItem('diff') > 0) {
      this.pauseDiff = Number(localStorage.getItem('diff'));
      this.run();
    }
  },
  methods: {
    run() {
      if (this.stage === 'Start') {
        this.stage = 'Pause';
        clearInterval(this.interval);
        this.startTime = moment();

        this.interval = setInterval(() => {
          this.diff = this.pauseDiff + moment().diff(this.startTime);
          this.saveLocal(this.diff);
        }, 1000);
      } else {
        this.pauseDiff = this.diff;
        this.stage = 'Start';
        clearInterval(this.interval);
      }
    },
    stop() {
      this.diff = 0;
      this.pauseDiff = 0;
      this.stage = 'Start';
      this.saveLocal(0);
      clearInterval(this.interval);
    },
    saveLocal(value) {
      localStorage.setItem('diff', value);
    },
  },
  computed: {
    time() {
      return moment.utc(this.diff).format('HH:mm:ss');
    },
  },
};
</script>

<style scoped>
  button {
    border: none;
    cursor: pointer;
    background: #444;
    color: #fff;
    padding: 20px;
    font-size: 18px;
    margin: 20px;
  }

  p {
    font-size: 20px;
  }
</style>
