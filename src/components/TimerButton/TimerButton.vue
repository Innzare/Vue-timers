<template>
   <button class="button" @click="$emit('onClick')">
      <StartIcon v-if="isStartType" />
      <ResetIcon v-if="isResetType" />
      <PauseIcon v-if="isPauseType" />
   </button>
</template>

<script>
import StartIcon from '../Icons/StartIcon.vue';
import ResetIcon from '../Icons/ResetIcon.vue';
import PauseIcon from '../Icons/PauseIcon.vue';
import { TIMER_BUTTON_TYPE } from '@/consts/timer';

export default {
name: 'TimerButton',
components: {
   StartIcon,
   ResetIcon,
   PauseIcon
},

props: {
   type: {
      type: String,
      isRequired: true
   },

   onClick: {
      type: Function,
      isRequired: true
   }
},

data() {
   return {};
},

computed: {
   isStartType() {
      return this.type === TIMER_BUTTON_TYPE.START
   },

   isResetType() {
      return this.type === TIMER_BUTTON_TYPE.RESET
   },

   isPauseType() {
      return this.type === TIMER_BUTTON_TYPE.PAUSE
   },
}
};
</script>

<style lang="scss">
.button {
   width: 40px;
   height: 40px;
   display: flex;
   justify-content: center;
   align-items: center;
   border: none;
   border-radius: 4px;
   padding: 8px;
   cursor: pointer;
   transition: all 0.3s;
   background-color: transparent;

   svg {
      fill: #fff
   }

   &.disabled {
      svg {
         fill: #9E9E9E
      }
   }

   &:hover {
      background-color: rgb(146, 146, 146);
   }
}
</style>