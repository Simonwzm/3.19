<template>
  <div class="login">
      <sidebar v-bind:elements="elements" v-bind:isShow="isShow&&start"></sidebar>
      <h1>Login to your Noteapp</h1>
      <form action="">
          Username: <br>
          <input type="text" name="username" v-model="Username">
          <br>
          Password: <br>
          <input type="text" name="password" v-model="password">
      </form>

      <div id="Hello" v-if="seen">Hello, {{isShow}}!</div>
      <div id="funny" v-if="seen" >Your password is not <span v-html="someHtml" style="color:orange"></span></div>
      <div class="btn_container">
      <router-link to="/auth/register">
            <button id="btn_toregister" >To register</button>
      </router-link>
      <button id="btn_login" v-on:click="func_post">Login</button>
      
      </div>
      <div id="recover">
          <a href="">Forget password?</a>
      </div>
      <button v-on:click="isShow=!isShow" style="float: right"></button>
  </div>
</template>

<script>

    import sidebar from "@/components/sidebar.vue";
    import axios from 'axios'
    export default  {
        components: {
            sidebar,
        },
        data: function() {
            return {
                Username: "",
                password: "",
                elements: [
                    {
                    id: 1,
                    text: "Home",
                    url: "/",
                    },
    
                ],
                position: 10,
                start:false,
            }
        },
        mounted () {
                let c = document.querySelector('#app')
                c.addEventListener('mousemove', this.onMouseMove);
                //增加锁扣，防止初始弹窗打开    
                this.start=false;
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
            },
            isShow : function() {
                if (this.position < 150 ) {
                    this.start=true
                    return true;
                }
                else {
                    return false;
                }
            }
        },
        methods: {
            func_post: function() {
                console.log(this.finish)
              if (this.finish) {
                  console.log({"username": this.Username, "password": this.password})
                  axios.post('http://127.0.0.1:8000/auth/login',{
                    "username": this.Username,
                    "password": this.password
                  }).then(function(response) {
                      console.log(response.data["token"]);
                  }).catch(function (error) {
                      console.log(error)
                  })
              } else {
                  alert('Please complete your form')
              } 
            },
            func_toregi: function() {
                console.log('not written yet')
            },
            onMouseMove: function(event) {
                this.position = event.clientX;
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
    height: 100vh;
    #Hello {
        padding: 1rem 0 .5rem 0;
    }
    input {
        margin-bottom: .5rem ;
    }
    @media screen and (max-width:500px){
        .btn_container{
            box-sizing: border-box;
            margin: 1.5rem auto .5rem auto;
            display: flex;
            width:170px;
            align-items: center;
            justify-content: center;
            flex-direction:column;
            a {
                width:100%;
                height: 5vh;
                margin-bottom:7%;
            }
        }
        #btn_login {
            width:100%;
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
        #btn_toregister {
            background-color: white;
            border: 1px solid #42b983;
            border-radius: .5rem;
            color: #42b983;
            height: 5vh;
            width: 100%;
            margin-bottom: 7%;
            box-sizing: border-box;
        }
        #btn_login:hover{
            color:white;
            background-color:#42b983;
            

        }
        #recover {
            font-size: .7rem;
            text-align:right;
            width:150px;
            margin-left: auto;
            margin-right: auto;
        }
    }
    @media only screen and (min-width:500px) {
        .btn_container{
            box-sizing: border-box;
            margin: 1.5rem 0 .5rem 0;
            height: 7vh;
            display: flex;
            width:400px;
            align-items: center;
            justify-content: center;
            margin-left:auto;
            margin-right:auto;
            flex-direction:row-reverse;
            a {
            width: 40%;
            height: 5vh;
            }
            #btn_login {
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
            #btn_toregister {
                margin-left:7%;
                background-color: white;
                border: 1px solid #42b983;
                border-radius: .5rem;
                color: #42b983;
                height: 5vh;
                width: 100%;
                box-sizing: border-box;
            }
            #btn_login:hover{
                color:white;
                background-color:#42b983;
                

            }
        }
        #recover {
            font-size: .7rem;
            text-align:right;
            width:340px;
            margin-left: auto;
            margin-right: auto;
        }
    }
}


</style>