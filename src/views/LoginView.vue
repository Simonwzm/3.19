<template>
  <div class="login">
      <h1>Login to your Noteapp</h1>
      <form action="">
          Username: <br>
          <input type="text" name="username" v-model="Username">
          <br>
          Password: <br>
          <input type="text" name="password" v-model="password">
      </form>

      <div id="Hello" v-if="seen">Hello, {{Username}}!</div>
      <div id="funny" v-if="seen" >Your password is not <span v-html="someHtml" style="color:orange"></span></div>
      <div class="btn_container">
      <button id="btn_toregister" v-on:click="func_toregi">To register</button>
      <button id="btn_login" v-on:click="func_post">Login</button>
      
      </div>
      <div id="recover">
          <a href="">Forget password?</a>
      </div>
  </div>
</template>

<script>
    import axios from 'axios'
    export default  {
        data: function() {
            return {
                Username: "",
                password: ""
            }
        },
        computed: {
            seen: function() {
                return (this.Username==="" || this.password==="")?false:true
            },
            someHtml: function() {
                return (this.password.split('').reverse().join(''))
            },
            finish: function() {
                if (this.Username!="" && this.password!="" ){
                    return true
                } else {
                    return false
                }
            }
        },
        methods: {
            func_post: function() {
                console.log(this.finish)
              if (this.finish) {
                  axios.post('http://127.0.0.1:8000/auth/login',{
                    "Access-Control-Allow-Origin": "http://127.0.0.1/auth/login",
                    "username": this.Username,
                    "password": this.password
                  }).then(function(response) {
                      console.log(response);
                  }).catch(function (error) {
                      console.log(error)
                  })
              } else {
                  alert('Please complete your form')
              } 
            },
            func_toregi: function() {
                console.log('not written yet')
            }
        }

    }

</script>

<style lang = 'scss' scoped>
.login {
    background-color: aliceblue;
    height: 80vh;
    box-sizing: border-box;
    padding-top: 1rem;
    #Hello {
        padding: 1rem 0 .5rem 0;
    }
    .btn_container{
        box-sizing: border-box;
        margin: 1.5rem 0 .5rem 0;
        height: 7vh;
        display: flex;
        width:40%;
        align-items: center;
        justify-content: center;
        margin-left:30%;
        margin-right:30%;
         
    }
    #btn_toregister {
        width: 40%;
        height: 5vh;
        background-color: white;
        border: 1px solid #42b983;
        border-radius: .5rem;
        color: #42b983;
    }
    #btn_toregister:hover{
        color:white;
        background-color:#42b983;

    }
    #btn_login {
        width: 40%;
        margin-left:7%;
        height: 5vh;
        background-color: white;
        border: 1px solid #42b983;
        border-radius: .5rem;
        color: #42b983;
    }
    #btn_login:hover{
        color:white;
        background-color:#42b983;

    }
    #recover {
        text-align:right;
        margin-top:.5rem;
        width: 35%;
        margin: 0 32.5% 0 32.5%;
        font-size: .7rem;
        a {color:gray}
    }
}


</style>