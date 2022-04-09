<template>
    <div class="container">
        <sidebar v-bind:elements="elements" v-bind:isShow="isShow&&start"></sidebar>
        <div class="shell">
            <div class="box-left">
                <h2>Login</h2>
                <p class="scription">
                    Tips: Try moving the mouse to the left end of the page~
                </p>
            </div>
            <div class="box-right">
                <form action="" class="form">
                    <label for="username">Username</label>
                    <input type="text" name="username" v-model="Username"/>
                    <label for="password">Password</label>
                    <input type="text" name="password" v-model="password"/>
                </form>
                <div class="btnc">
                    <button  v-on:click="func_post">Login</button>
                    <button  v-on:click="func_post">Register</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import sidebar from "@/components/sidebar.vue";
export default {
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
                {
                    id:2,
                    text:"Forget Password?",
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
        finish: function() {
            if (this.Username!="" && this.password!="" ){
                return true
            } else {
                return false
            }
        },
        isShow : function() {
            if (this.position < 150 ) {
                this.start=true;
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

<style  lang="scss" scoped>
.container {
    height: 100vh;
    width: 100vw;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    z-index:1;
    background: inherit;    
    // font-family: "ubuntu", sans-serif;
}
.container::after {
    content: "";
    width:100%;
    height:100%;
    position: absolute;
    left:0;
    top:0;
    filter: blur(5px);
    /* background:linear-gradient(to right top, rgba(0,0,0,0.1), rgba(0,0,0,0,5)); */
    background: inherit;
    z-index: -1;
}
.shell {
    height: 60vh;
    width: 57%;
    display: flex;
    flex-direction: row;
}
.box-left {
    width: 40%;
    height: 80%;
    position: relative;
    top: 10%;
    left: 0;
    background-color: rgba(255,255,255,0.75);
    border-radius: 10px 0 0 10px;
    h2 {
        font-size: 3rem;
        color: black;
        margin: 3.5rem 0 1.5rem 4rem;
    }
    p {
        display: block;
        color: rgb(143, 94, 135);
        font-size: 1.5rem;
        margin: 3rem 2.5rem 1rem 4rem;
    }
}
.box-right {
    width: 55%;
    height: 100%;
    background-color: rgba(184, 115, 200, 0.8);
    position: relative;
    border-radius: 0 10px 10px 0;
}
.form {
    margin: 3rem 4rem;
    display: flex;
    flex-direction: column;
    justify-content: start;
    align-items: start;
    box-sizing: border-box;
    width: 70%;

}
label {
    display: block;
    margin: 1rem 0;
    font-size: 1.6rem;
    color: rgb(241, 241, 241);
    position: relative;
    width: 100%;
    font-weight: 100;
}
label::before {
    content: '';
    display: block;
    width: 100%;
    position: absolute;
    top:90px;
    height: 3px;
    background-image: linear-gradient(to right, #44ffff, #b888ff);
}
input {
    background: transparent;
    border: 0;
    line-height: 1.5rem;
    width: 100%;
    color: #f2f2f2;
    font-size: 1.5rem;
    margin-bottom: 1.5rem;
}
input:focus {
    outline:4px solid rgba(143,94,135,0.5);
    border-radius: .5rem;
    outline:4px solid rgba(143,94,135,0.5);
}

.btnc {
    margin: 1rem 4rem;
    width: 70%;
    height: 6vh;
    display: flex;
    flex-direction: row;
    justify-content: right;
}
button {
    background: rgb(143, 94, 135);
    color: white;
    font-size: 1rem;
    width: 30%;
    border: 0;
    border-radius: .5rem;
    text-align:center;
    margin: 0rem 0rem 0rem 1rem;
    cursor: pointer;
    outline:0;
    font-weight: bold;  
}
button:hover {
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.479);
    transition: box-shadow .2s;
}
</style>