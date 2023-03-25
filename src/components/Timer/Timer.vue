<template>
   <div :class="timer.isRunning ? 'timer' : 'timer timer-off'">
      <span class="timer-remove" @click="$emit('onRemoveTimer', timer)">+</span>

      <div class="timer-display">
         {{ formatTime(timer.timePassed) }}
      </div>

      <div class="timer-divider" />

      <div class="timer-controls">
         <TimerButton
            :class="timer.isRunning ? '' : 'disabled'"
            :type="timer.isRunning ? 'PAUSE' : 'START'"
            @onClick="$emit(`${timer.isRunning ? 'onPauseTimer' : 'onStartTimer'}`, timer)"
         />
         <TimerButton
            :class="timer.isRunning ? '' : 'disabled'"
            type="RESET"
            @onClick="$emit('onResetTimer', timer)"
         />
      </div>
   </div>
</template>

<script>
import TimerButton from '../TimerButton';
import { TIMER_TYPE } from '@/consts/timer';

export default {
   name: 'Timer',
   components: {
      TimerButton
   },
   props: {
      timer: {
         type: Object,
         required: true
      }
   },

   computed: {
      formatTime() {
         return function (timePassed) {
            const seconds = timePassed % 60;
            const minutes = Math.floor(timePassed / 60) % 60;
            const hours = Math.floor(timePassed / 3600);

            switch (true) {
               case this.timer.timerType === TIMER_TYPE.SECONDS:
                  return `${seconds.toString().padStart(2, '0')}`;

               case this.timer.timerType === TIMER_TYPE.MINUTES:
                  return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            
               default:
                  return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;;
            }
         }
      }
   },
};
</script>

<style lang="scss" scoped>
.timer {
   position: relative;
   display: flex;
   flex-direction: column;
   align-items: center;
   width: 225px;
   background-color: #696969;
   border-radius: 4px;

   .timer-remove {
      position: absolute;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 18px;
      top: 5px;
      right: 7px;
      color: #fff;
      font-weight: bold;
      cursor: pointer;
      transform: rotate(45deg);
   }

   .timer-display {
      display: block;
      font-size: 22px;
      padding: 16px 8px;
      color: #fff;
   }

   .timer-divider {
      width: 100%;
      height: 1px;
      background-color: #fff;
   }

   .timer-controls {
      display: flex;
      gap: 36px;
      padding: 16px 8px;
   }

   button {
      font-size: 16px;
      padding: 5px 10px;
      margin-bottom: 0;
   }
}

.timer-off {
   .timer-display {
      color: #9E9E9E
   }

   .timer-divider {
      background-color: #9E9E9E;
   }
}
</style>