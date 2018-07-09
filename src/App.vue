<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style lang="scss">
@mixin flex {
    display: flex;
}

@mixin size($width, $height) {
    width: $width;
    height: $height;
}

html {
    @include size(100%, 100%);
}
body {
    @include size(100%, 100%);
    @include flex;
    align-items: center;
    justify-content: center;
    margin: 0px;

    div {
        @include flex;
        flex-direction: column;
    }
}
#app {
    @include size(100%, 100%);
    font-family: 'SEGOE UI', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #333;
}
</style>
