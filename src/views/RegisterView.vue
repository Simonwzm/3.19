<template>
  <div class="register">
      <h1>Start your Noteapp experience!</h1>
      <form action="">
          Username: <br>
          <input type="text" name="username" v-model="Username">
          <br>
          Password: <br>
          <input type="text" name="password" v-model="password">
          <br>
          <div id="af" v-if="enterpassword">
            Please affirm your password: <br>
            <input type="text" name="afpsw" v-model="afpsw" v-if="enterpassword" v-on:change="pswcheck">
            <div v-if="wrongPsw" style="color: red; margin-bottom: .5rem">Unmatched password entered </div>
          </div>
          Email: <br>
          <input type="text" name="email" v-model="email" v-on:change="examine">
          <div v-if="wrongEm" style="color:red; margin-bottom:.5rem">Not a valid email address!</div>
      </form>

      <!-- <div id="Hello" v-if="seen">Hello, {{Username}}!</div>
      <div id="funny" v-if="seen" >Your password is not <span v-html="someHtml" style="color:orange"></span></div> -->
      <div class="btn_container">
      <button id="btn_toregister" v-on:click="func_regi">Register</button>
      <router-link to="/auth/login">
        <button id="btn_login" v-on:click="func_tolgin">To login</button>
      </router-link> 
      </div>
  </div>
</template>

<script>
    import axios from "axios";
    export default  {
        data: function() {
            return {
                Username: "",
                password: "",
                email: "",
                afpsw: "",
                wrongEm: false,
                wrongPsw: false,
            }
        },
        computed: {
            seen: function() {
                return (this.Username==="" || this.password==="")?false:true
            },
            someHtml: function() {
                return (this.password.split('').reverse().join(''))
            },
            enterpassword: function() {
                if (this.password != "") {
                    return true;
                } else {
                    return false;
                }
            },
            finish: function() {
                if (this.Username != "" && this.password != "" && this.email != "" && this.wrongEm === false && this.wrongPsw === false) {
                    return true;
                } else {
                    return false;
                }
            }
        },
        methods: {
            examine: function() {
                var reMail =/\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*/;
                if (!reMail.test(this.email)) {
                    this.wrongEm = true
                    console.log('not a valid email')
                }
                else {
                    this.wrongEm = false
                }
                return;
            },
            pswcheck: function() {
                if (this.afpsw === this.password) {
                    this.wrongPsw = false
                } else {
                    this.wrongPsw = true
                }
                return;
            },
            func_regi: function() {
                if (this.finish === true) {
                    axios.post('http://127.0.0.1:8000/auth/register', {
                        "email": this.email,
                        "username": this.Username,
                        "password": this.password,
                    }).then(function(response) {
                        console.log(response);
                    }).then(function(error) {
                        console.log(error);
                    })
                } else {
                    alert("Please check your form");
                }
            },
            func_tolgin: function() {

            }
        }
    }

</script>

<style lang = 'scss' scoped>
.register {
    background-color: aliceblue;
    height: 80vh;
    box-sizing: border-box;
    padding-top: 1rem;
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
            }
        }
        #btn_toregister {
            width:100%;
            height: 5vh;
            background-color: white;
            border: 1px solid #42b983;
            border-radius: .5rem;
            color: #42b983;
            margin-bottom:7%;
        }
        #btn_toregister:hover{
            color:white;
            background-color:#42b983;

        }
        #btn_login {
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
        #btn_toregister {
            width: 40%;
            height: 5vh;
            background-color: white;
            border: 1px solid #42b983;
            border-radius: .5rem;
            color: #42b983;
            margin-left:7%;
        }
        #btn_toregister:hover{
            color:white;
            background-color:#42b983;

        }
        #btn_login {
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
        
    }
}


</style>