<template>
  <div id="app">
    <!-- <nav>
      <router-link to="/auth/login">Login</router-link> |
      <router-link to="/auth/register">register</router-link>

    </nav> -->
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  // background-image: linear-gradient(to bottom right, #bdbef8, #9a9bee);
  background-image: url("@/assets/ipexels-pixabay-33545.jpg");
  background-size: cover;
  width: 100%;
}

body {
  margin: 0;
  height: 100vh;
}
</style>
