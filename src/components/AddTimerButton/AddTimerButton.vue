<template>
   <button class="button" @click="$emit('onClick')">+</button>
 </template>
 
 <script>
 export default {
   name: 'AddTimerButton',
   props: {
     onClick: {
       type: Function,
       isRequired: true,
       default: () => {}
     }
   }
 };
 </script>
 
 <style lang="scss" scoped>
 .button {
   width: 225px;
   height: 120px;
   display: flex;
   justify-content: center;
   align-items: center;
   color: #fff;
   font-size: 32px;
   border: none;
   border-radius: 4px;
   padding: 8px;
   cursor: pointer;
   background-color: #696969;
   transition: all 0.3s;
   margin-bottom: 0;
 
   &:hover {
     background-color: #696969ab;
   }
 }
 </style>