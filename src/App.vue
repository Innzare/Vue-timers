<template>
   <div class='app-wrapper'>
      <div class="timer-actions-wrapper">
         <div class="timer-type-wrapper">
            <div class="timer-type-field">
               <input type="radio" id="hours" value="HOURS" v-model="timerType">
               <label for="hours">Часы</label>
            </div>

            <div class="timer-type-field">
               <input type="radio" id="minutes" value="MINUTES" v-model="timerType">
               <label for="minutes">Минуты</label>
            </div>

            <div class="timer-type-field">
               <input type="radio" id="seconds" value="SECONDS" v-model="timerType">
               <label for="seconds">Секунды</label>
            </div>
         </div>

         <AddTimerButton @onClick="addTimer" />
      </div>
      
      <div class="timers-wrapper">
         <Timer
            v-for="(timer) in timers"
            :key="timer.id"
            :timer="timer"
            @onStartTimer="startTimer"
            @onPauseTimer="pauseTimer"
            @onResetTimer="resetTimer"
            @onRemoveTimer="removeTimer"
         />
      </div>
   </div>
</template>

<script>
import Timer from './components/Timer';
import AddTimerButton from './components/AddTimerButton';
import { TIMER_TYPE } from '@/consts/timer';

export default {
   components: {
      Timer,
      AddTimerButton
   },

   data() {
      return {
         timers: [],
         timerType: TIMER_TYPE.HOURS
      };
   },

   methods: {
      addTimer() {
         this.timers.push(
            {
               timePassed: 0,
               isRunning: false,
               id: this.uniqueId(),
               timerType: this.timerType,
               timer: null
            }
         );
      },

      uniqueId() {
         return Date.now().toString(36) + Math.random().toString(36).substring(2);
      },

      startTimer(currentTimer) {
         if (!currentTimer.isRunning) {
            currentTimer.timer = setInterval(() => {
               currentTimer.timePassed++;
            }, 1000);

            currentTimer.isRunning = true;
         }
      },

      pauseTimer(currentTimer) {
         if (currentTimer.isRunning) {
            clearInterval(currentTimer.timer);
            currentTimer.isRunning = false;
         }
      },

      resetTimer(currentTimer) {
         currentTimer.timePassed = 0;
         currentTimer.isRunning = false;

         clearInterval(currentTimer.timer);
      },

      removeTimer(currentTimer) {
         this.timers = this.timers.filter(item => item.id !== currentTimer.id);
      }
   },
};
</script>

<style>
@import '@/assets/styles/global.scss';

.app-wrapper {
   width: 100%;
   height: 100vh;
   display: flex;
   flex-direction: column;
   justify-content: center;
   align-items: center;
}

.timer-type-wrapper {
   display: flex;
   flex-direction: column;
   gap: 8px;
   margin-bottom: 8px;
}

.timer-actions-wrapper {
   margin-bottom: 24px;
}

.timers-wrapper {
   display: flex;
   justify-content: center;
   flex-wrap: wrap;
   gap: 16px;
}

.timer-type-field {
   color: #fff;
}
</style>