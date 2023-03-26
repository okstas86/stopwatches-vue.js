<template>
  <div class="container">
    <div class="timer-wrap" v-for="(timer, index) in timers" :key="index">
      <div class="top-container">
        <div class="timer" :class="{ active: timer.isRunning }">
          {{ formatTime(timer.time) }}
        </div>
      </div>
      <div class="divider" :class="{ active: timer.isRunning }"></div>
      <div class="bottom-container">
        <img
          src="../assets/img/start.png"
          v-show="!timer.isRunning"
          alt="Start"
          @click="startTimer(index)"
          :disabled="timer.isRunning"
        />
        <img
          src="../assets/img/pause.png"
          v-show="timer.isRunning"
          alt="Pause"
          @click="pauseTimer(index)"
          :disabled="!timer.isRunning"
          :class="{ active: timer.isRunning }"
        />
        <img
          src="../assets/img/stop.png"
          alt="Stop"
          @click="resetTimer(index)"
          :disabled="timer.time === 0"
          :class="{ button: true, active: timer.isRunning }"
        />
      </div>
    </div>
    <div class="wrap-button" v-if="timers.length === 0">
      <img src="../assets/img/add.png" alt="Add timer" @click="addTimer" />
    </div>
    <div class="wrap-button" v-else>
      <img src="../assets/img/add.png" alt="Add timer" @click="addTimer" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      timers: [],
      timerIsActive: false,
      addNewTimer: false,
    };
  },
  methods: {
    addTimer() {
      this.timers.push({ time: 0, isRunning: false });
    },
    startTimer(index) {
      this.timers[index].isRunning = true;
      this.interval = setInterval(() => {
        this.timers[index].time++;
      }, 1000);
      this.timerIsActive = true;
    },
    pauseTimer(index) {
      this.timers[index].isRunning = false;
      clearInterval(this.interval);
    },
    resetTimer(index) {
      this.timers[index].time = 0;
      this.timers[index].isRunning = false;
      clearInterval(this.interval);
    },
    formatTime(time) {
      const hours = Math.floor(time / 3600);
      const minutes = Math.floor((time / 60) % 60);
      const seconds = time % 60;
      let formattedTime = "";

      if (hours > 0) {
        formattedTime += `${hours.toString().padStart(2, "0")}:`;
      }

      if (minutes > 0 || hours > 0) {
        formattedTime += `${minutes.toString().padStart(2, "0")}:`;
      }

      formattedTime += seconds.toString().padStart(2, "0");

      return formattedTime;
    },
  },
};
</script>
<style scoped>
.container {
  margin: 0 100px 0 100px;
  display: flex;
  flex-wrap: wrap;
  background-color: #353638;
}
.timer-wrap {
  background-color: #696969;
  width: 225px;
  height: 120px;
  flex-direction: column;
  color: #9e9e9e;
  position: relative;
  margin: 50px;
}

.top-container {
  width: 100%;
  height: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1;
}
.divider {
  width: 100%;
  height: 1px;
  background-color: #9e9e9e;
}
.bottom-container {
  width: 100%;
  height: 50%;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  z-index: 1;
}
.wrap img {
  margin-top: 15px;
}
.timer {
  font-size: 22px;
  position: absolute;
  margin-bottom: 20px;
  top: 20px;
}
.active {
  filter: brightness(200%);
}

.wrap-button {
  background-color: #696969;
  width: 225px;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 50px;
}

img {
  cursor: pointer;
}

@media (max-width: 768px) {
  .timer-wrap,
  .wrap-button {
    width: 225px;
    margin: 50px;
  }
}

@media (max-width: 420px) {
  .container {
    justify-content: center;
    margin: 0;
  }
  .timer-wrap,
  .wrap-button {
    width: 225px;
    margin: 10px;
  }
}
</style>
