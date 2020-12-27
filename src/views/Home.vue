<template>
  <div class="home">
    <!--<img alt="Vue logo" src="../assets/logo.png">-->
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <Login msg="login"></Login>
  </div>
</template>

<script>

/*import HelloWorld from '../components/HelloWorld'*/
import Login from "../components/Login";
export default {
  name: 'Home',
  components: {
    /*HelloWorld,*/
    Login
  }
}
</script>
