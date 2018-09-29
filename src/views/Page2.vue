<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png">
        <HelloWorld msg="Welcome to Your Vue.js App"/>
        <el-button>{{names}}</el-button>
    </div>
</template>

<script>
    export default {
        name: "Page2",
        data(){
            return{
                names:'page2'
            }
        }
    }
</script>

<style scoped>

</style>
