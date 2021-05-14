<template>
  <!-- Use a button to toggle animation -->
  <button type="button" @click="flag = !flag">Toggle</button>
  
  <!-- Animating with CSS Transitions -->
  <!-- <transition name="fade" mode="out-in">
    <h2 v-if="flag" key="main">Hello World!</h2>
    <h2 v-else key="secondary">Another Hello!</h2>
  </transition> -->

  <!-- Animating with CSS Animations -->
  <transition name="zoom" type="animation" appear>
    <h2 v-if="flag">Hello!</h2>
  </transition>

</template>

<script>
export default {
  name: "App",
  data() {
    return {
      flag: true,
    }
  }
};
</script>

<style>

h2 {
  width: 400px;
  padding: 20px;
  margin: 20px;
}

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

.zoom-enter-active {
  animation: zoom-in 1s linear forwards;
  transition: all 1s linear;
}

.zoom-leave-active {
  animation: zoom-out 1s linear forwards;
  transition: all 1s linear;
}

.zoom-enter-from {
  opacity: 0;
}

.zoom-leave-to {
  opacity: 0;
}

@keyframes zoom-in {
  from {
    /* scales it to its smallest size possible */
    transform: scale(0, 0); 
  }
  to {
    /* scales to its original size */
    transform: scale(1, 1);
  }
}

/* reverse of zoom-out */
@keyframes zoom-out {
  from {
    transform: scale(1, 1); 
  }
  to {
    transform: scale(0, 0);
  }
}

</style>
