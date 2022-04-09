<template>
    <div class="sidebar" :class="isShow?'show':'hide'">
        <div class="container" >
            <!-- 必须使用:keys -->
            <!-- 使用v:bind来使用表达式 -->
            <router-link class="el" v-for="el in elements" :key="el.id" v-bind:to="el.url" >
                <button class="e">
                    {{el.text}}
                </button>
            </router-link> 
        </div>

    </div>
</template>

<script>
    export default {
        name: "sidebar",
        props: {
            elements:[],
            isShow:false,
        },
        // 不是data{function}
        data: function() {
                return {
                    position: 10,
                }
            }
        ,
    }

</script>

<style scoped>
.sidebar {
    height: 100vh;
    position: absolute;
    top:0;
    left:0;
    width: 20%;
    background-color: rgba(0,0,0,0.15);
    box-sizing: border-box;
    transition: all 0.3s;
    transition-delay: 0.2s;
    z-index: 10;
}
.container {
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top:0;
}
.show {
    transform: translateX(0);
}
.hide {
    transform: translateX(-100%);
}

.el {
    text-align: center;
    height: 10vh;
    width: 100%;
    border-radius: 1em;
}
.e {
    text-align: center;
    width: 100%;
    height: 100%;
    border: none;
    color: white;
    font-size: 1.2rem;
    font-family: "ubuntu";
    cursor: pointer;
    background-color: rgba(0,0,0,0);
}
.e:hover {
transition: background-color .5s;
background-color: rgba(0,0,0,0.2);
}
</style>