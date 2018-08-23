<template>
    <div>
    <Loading></Loading>
    </div>
</template>

<script>
import Loading from "./Loading.vue";

export default {
  name: 'Home',
  data() {
    return {

    }
  },
  components: {
    Loading: Loading,
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
#canvas {
  position: absolute;
  left: 0;
  top: 0;
}
</style>
