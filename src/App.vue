<template>
  <div class="main" >
    <div class="main-router">
      <router-view />
    </div>
  </div>
</template>

<style lang="scss">
#app {
    background: #F7F7F7;
    width: 100vw;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: stretch;
}

.main {
    background: #F5F5F5;
    min-height: 100vh;
    min-width: 100vw;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    &-router {
        flex-grow: 1;
    }
}
</style>