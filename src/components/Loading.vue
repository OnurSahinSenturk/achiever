<template>
    <div id="loading">
        <div class="circle inner"></div>
        <div class="circle outer"></div>
        <div class="layer"></div>
    </div>
</template>

<script>
export default {
  name: "Loading",
  data() {
    return {};
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#loading {
  position: fixed;
  width: 50px;
  height: 50px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border-radius: 50px;

  .circle {
    position: absolute;
    width: 100%;
    height: 100%;
    opacity: 0.7;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    border-radius: 50px;

    &.inner {
      background: #777;
      animation: loading 5s infinite;
    }

    &.outer {
      background: #777;
      animation: loading 5s infinite backwards;
    }
  }
}

@keyframes loading {
  0%,
  100% {
    width: 0%;
    height: 0%;
  }

  50% {
    width: 100%;
    height: 100%;
  }
}
</style>
