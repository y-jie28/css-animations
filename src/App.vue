<template>
  <!-- Use a button to toggle animation -->
  <button type="button" @click="flag = !flag">Toggle</button>
  
  <!--  -->
  <transition name="fade" mode="out-in">
    <h2 v-if="flag" key="main">Hello World!</h2>
    <h2 v-else key="secondary">Another Hello!</h2>
  </transition>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      flag: false,
    }
  }
};
</script>

<style>
/* initial frame */
.fade-enter-from {
  opacity: 0;
}

/* added entirely, this should be where transition rules are added */
.fade-enter-active {
  transition: all 1s linear;
}

.fade-leave-to {
  transition: all 1s linear;
  opacity: 0;
}


</style>
