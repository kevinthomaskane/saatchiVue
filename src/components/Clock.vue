<template>
    <div v-if="seconds" class="clock">
        <div class="hours">
            {{hours}}
        </div>
        <div class="minutes">
            {{minutes}}
        </div>
        <div class="seconds">
            {{seconds}}
        </div>
    </div>
</template>

<script>
export default {
  name: 'Clock',
  data() {
    return {
      hours: '',
      minutes: '',
      seconds: ''
    }
  },
  mounted() {
    const date = new Date()
    this.hours = this.getStandardHours(date.getHours())
    this.minutes = this.addZero(date.getMinutes())
    this.seconds = this.addZero(date.getSeconds())
    setInterval(this.increaseSeconds, 1000)
  },
  methods: {
    addZero(time) {
      if (time < 10) {
        return '0' + time
      } else {
        return time
      }
    },
    increaseSeconds() {
      let secs = parseInt(this.seconds)
      if (secs < 59) {
        if (secs < 9) {
          secs++
          this.seconds = '0' + secs
          return
        }
        secs++
        this.seconds = secs
      } else {
        this.increaseMinutes()
        secs = '00'
        this.seconds = secs
      }
    },
    increaseMinutes() {
      let mins = parseInt(this.minutes)
      if (mins < 59) {
        if (mins < 9) {
          mins++
          this.minutes = '0' + mins
          return
        }
        mins++
        this.minutes = mins
      } else {
        this.increaseHours()
        mins = '00'
        this.minutes = mins
      }
    },
    increaseHours() {
      let hrs = parseInt(this.hours)
      if (hrs < 12) {
        if (hrs === 0) {
          this.hours = '12'
          return
        }
        hrs++
        this.hours = hrs
      } else {
        hrs = '1'
        this.hours = hrs
      }
    },
    getStandardHours(hrs) {
      if (hrs < 13) {
        return hrs
      } else {
        return hrs - 12
      }
    }
  }
}
</script>

<style lang="scss">
.clock {
  color: white;
  width: auto;
  display: inline-block;
  text-align: center;
  padding: 5px;
  border-radius: 5px;
  font-family: 'Quicksand', sans-serif;
  position: fixed;
  top: 10px;
  right: 10px;
  & > div {
    display: inline-block;
    font-size: 20px;
    padding: 0 5px;
    position: relative;
    text-shadow: 1px 2px 1px rgba(0, 0, 0, 0.5);
  }
  .hours::after {
    content: ':';
    font-size: 16px;
    line-height: 23px;
    vertical-align: top;
    position: absolute;
    right: -2px;
    top: 0;
  }
  .seconds::after {
    content: ':';
    font-size: 16px;
    line-height: 23px;
    vertical-align: top;
    position: absolute;
    left: -3px;
    top: 0;
  }
  .seconds {
    padding-left: 3px;
  }
}
</style>
