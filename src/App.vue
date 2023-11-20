<template>
  <!--<nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link> |
    <router-link to="/signup">SignUp</router-link> |
    <router-link to="/login">LogIn</router-link>
  </nav>-->
  <div id="router" class="w-100 ">
  <nav class="p-md-3 navbar navbar-expand-lg navbar-dark">
  <a class="navbar-brand" href="#">BigO</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class=" pl-5 collapse navbar-collapse" id="navbarSupportedContent">
    <ul class=" navbar-nav mr-auto">
      <li class="nav-item">
        <router-link class="nav-link" to="/">Home</router-link>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Course
        </a>
        <div class="dropdown-menu bg-dark" aria-labelledby="navbarDropdown">
          <router-link class="dropdown-item" to="/enroll">How to enroll</router-link>
          <div class="dropdown-divider"></div>
          <router-link class="dropdown-item" to="/ICT10001">Problem Solving with ICT</router-link>
          <router-link class="dropdown-item" to="/COS10005">Web Development</router-link>
          <router-link class="dropdown-item" to="/INF10002">Database Analysis and Design</router-link>
          <router-link class="dropdown-item" to="/COS10009">Introduction to Programming</router-link>
        </div>
      </li>
      <li v-if="account==false" class="nav-item">
        <router-link class="nav-link" to="/login">Log In</router-link>
      </li>
      <li v-if="account==false" class="nav-item">
        <router-link class="nav-link" to="/signup">Sign Up</router-link>
      </li>
      <li v-if="account==true" class="nav-item">
        <router-link class="nav-link" to="/user">My Enrollment</router-link>
      </li>
      <li v-if="account==true" class="nav-item">
        <button @click="logOut" class="nav-link align-center">Log Out</button>
      </li>
    </ul>
  </div>
  </nav>
  </div>
  <router-view/>
</template>

<script>
  export default { //json file location
  data: function()
  {
    return{
      name: localStorage.getItem("user-name"),
      email: localStorage.getItem("user-email"),
      password: localStorage.getItem("user-pwd"),
      account: false
    }
  },


  mounted(){
    if(this.name)
    {
      this.account = true;
    }
  },

  methods:{
    logOut(){
      localStorage.removeItem("user-name");
      localStorage.removeItem("user-email");
      localStorage.removeItem("user-pwd");
      this.$router.go({
      path: "/",
      force: true
      });
    }
  }
 }
</script>

<style>
nav {
  /*font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;*/
  text-align: center;
  color: #ebf0f5;
  background-color: rgb(0, 0, 0);
}

@media only screen and (min-width: 850px)
{
  nav {
    font-size: 20px;
  }
  .nav-link{
    margin-right: 10px;
  }
}

.dropdown-item{
  color:rgb(186, 183, 183);
}

body{
  text-align: center;
  background-color: rgb(0, 0, 0);
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}



</style>
