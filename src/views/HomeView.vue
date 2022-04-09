<template>
  <!-- <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div> -->
  <div class="home">
    <div class="container">
      <div class="text">
        <div class="title">Welcome to <span class="tt">NoteApp</span>!</div>
        <div class="subtitle">A cloud-based notes management website</div>
      </div>
      <div class="navg">
        <div class="btn_ctn">
          <router-link to="/login">
            <button id="login">Login</button>
          </router-link>
          <router-link to="/register">
            <button id="register">Register</button>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
export default {
  // name: 'HomeView',
  // components: {
  //   HelloWorld
  // }

}
</script>

<style lang="scss" scoped>
.home {
  height: 100vh;
  width: 100%;
  // justify-content: center;
  flex-direction: column;
  align-items: center;
  display: flex;
  background-image: url("@/assets/ipexels-pixabay-33545.jpg");
  background-size: cover;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 80vh;
  width: 70%;
  margin-top: 10vh;
  background-color: rgba(0,0,0,0.1);
  border-radius: 1rem;
}
.text {
  width: 100%;
  text-align:center;
  height: 45vh
}
// .icon {
//   width: 10vh;
//   height: 10vh;
//   text-align: center;
//   img {
//     width: 100%;
//     height: 100%;
//   }
// }

.title {
  font-size: 5rem;
  font-weight: bold;
  color: white;
  font-family: 'Ubuntu', sans-serif;
  margin-top: 15vh;
  margin-bottom: 7vh;
  .tt {
    
  }
}
.subtitle {
  font-size: 2.2rem;
  color: white;
  font-family: 'Courgette', cursive;
}
.navg {
height:35vh;
width: 100%;
background-color: rgba(255,255,255,0.1);
}
.btn_ctn {
margin-top: 5vh;
display: flex;
flex-direction: row;
justify-content: space-evenly;
align-items: center;
}
a {
  width: 30%;
  height: 12vh;
  border: 2px solid  rgba(255,255,255,0.5);
  border-radius: .5rem;
}
button#login , button#register {
  width: 100%;
  height: 100%;
  background-color: rgba(255,255,255,0.01);
  color: white;
  font-size: 1.5rem;
  font-family: 'Ubuntu', sans-serif;
  border: none;
}

button#login:hover , button#register:hover {
  transition: background-color 0.75s, border 0.75s, font-size 0.75s;
  background-color: rgba(255,255,255,0.15); 
  font-size: 1.7rem;
  cursor: pointer;
}

a:hover {
  transition: border 0.75s;
  border: 2px solid rgba(255,255,255,0.75);
}

</style>