<template>
  <!--<div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>-->
  <div id="home">
    <h1 id="header">BIG-O CODING</h1>
    <h4>Learn Coding with Experts</h4>
    <button v-if="account==false"  v-on:click="logIn" type="button" class=" m-4 py-2 px-8 px-md-15">Log In</button>
    <button v-if="account==false"  v-on:click="signUp" type="button" class=" m-4 py-2 px-8 px-md-15">Sign Up</button>
  </div>
  <div id="about">
    <h1>WHY STUDY CODING?</h1>
    <div class="row m-4">
      <div class="col-md-3">
        <h3>Coding can boost problem solving skills</h3>
        <img src="../assets/reason1.png" alt="img" class = "img-responsive" >
        <p>Outside from the implications of coding which look good on a resume, coding actually does boost skills which are actually useful to most jobs. Problem solving and logic are the main two. Learning to code is like an exercise session for the “left” side of the brain.</p>
      </div>
      <div class="col-md-3">
        <h3>Coding improves interpersonal skills</h3>
        <p>Coding for most big projects tends to be a collaborative effort. This means having to work as one cog as part of a greater team. Learning how to best interact with bosses and co-workers is an essential work skill, and it can often be developed through coding.</p>
        <img src="../assets/reason2.png" alt="img" class = "img-responsive" >
      </div>
      <div class="col-md-3">
        <h3>Coding could lead to freelance work</h3>
        <img src="../assets/reason3.png" alt="img" class = "img-responsive">
        <p>If you are wanting to go freelance, or have the ability to work while traveling, coding may be a great way to get into this. As coding is a highly valued skill at the moment, many companies are willing to outsource the work. This means skilled coders have the ability to create their own schedule.</p>
      </div>
      <div class="col-md-3">
        <h3>Coding allow to pursue passion projects</h3>
        <p>Coding is a fantastic skill for you if you are the sort of person who has tons of ideas and wants to get started on everything yesterday. Not having to look elsewhere for a coder saves both time and money, plus it means you can keep changing and redesigning as your idea develops.</p>
        <img src="../assets/reason4.png" alt="img" class = "img-responsive" >
      </div>
    </div>
  </div>

  <div id="course">
    <h1>OUR CODING COURSE</h1>

    <div id="carouselExampleControls" class="carousel slide" data-ride="carousel">

    <div class="carousel-inner">
      <div class="carousel-item active">
        <p>BigO Coding is foundations of software engineering program equips our students with the foundational knowledge and skills needed to become entry software engineers & developers.</p>
        <p>Through a project-led and cohort-based pedagogy, Our students learn how to walk, talk and think like software engineers as they embark on a 9-month (full-time) or 18-month (part-time) journey</p>
        <a href='http://localhost:8080/enroll'><button id="enroll" type="button" class=" m-1 py-3 px-2 px-md-10">Find out more</button></a>
      </div>
      <div  v-for="m in msg" v-bind:key="m.id" class="carousel-item">
        <p>{{m.code}}</p>
        <h5 class="text-red">{{m.desc}}</h5>
        <p class="text-justify">{{m.aim}}</p>
        <button @click="viewCourse(m.code)"  type="button" class="py-3 px-2 px-md-10 text-white">Enroll Now</button>
      </div>
    </div>
    <a class="carousel-control-prev" href="#carouselExampleControls" role="button" data-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleControls" role="button" data-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
    </div>
  </div>

  <footer class="pt-5 pb-5 row">
  <div id="logo" class="col-6 mt-5">
    <h4><img src="../assets/logo.jpg" alt="image" width="30%">
    BigO Coding</h4>
    <p class="mx-5">In the spirit of reconciliation, BigO Coding School acknowledges the Traditional Custodians of country throughout Australia and their connections to land, sea and community.</p>
  </div>
  <div id="contact" class="text-center col-6">
    <h2 class="mt-5">Contact us</h2>
    <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class=" bi bi-facebook m-2" viewBox="0 0 16 16">
        <path d="M16 8.049c0-4.446-3.582-8.05-8-8.05C3.58 0-.002 3.603-.002 8.05c0 4.017 2.926 7.347 6.75 7.951v-5.625h-2.03V8.05H6.75V6.275c0-2.017 1.195-3.131 3.022-3.131.876 0 1.791.157 1.791.157v1.98h-1.009c-.993 0-1.303.621-1.303 1.258v1.51h2.218l-.354 2.326H9.25V16c3.824-.604 6.75-3.934 6.75-7.951z"/>
    </svg>
    <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class=" bi bi-instagram m-2" viewBox="0 0 16 16">
        <path d="M8 0C5.829 0 5.556.01 4.703.048 3.85.088 3.269.222 2.76.42a3.917 3.917 0 0 0-1.417.923A3.927 3.927 0 0 0 .42 2.76C.222 3.268.087 3.85.048 4.7.01 5.555 0 5.827 0 8.001c0 2.172.01 2.444.048 3.297.04.852.174 1.433.372 1.942.205.526.478.972.923 1.417.444.445.89.719 1.416.923.51.198 1.09.333 1.942.372C5.555 15.99 5.827 16 8 16s2.444-.01 3.298-.048c.851-.04 1.434-.174 1.943-.372a3.916 3.916 0 0 0 1.416-.923c.445-.445.718-.891.923-1.417.197-.509.332-1.09.372-1.942C15.99 10.445 16 10.173 16 8s-.01-2.445-.048-3.299c-.04-.851-.175-1.433-.372-1.941a3.926 3.926 0 0 0-.923-1.417A3.911 3.911 0 0 0 13.24.42c-.51-.198-1.092-.333-1.943-.372C10.443.01 10.172 0 7.998 0h.003zm-.717 1.442h.718c2.136 0 2.389.007 3.232.046.78.035 1.204.166 1.486.275.373.145.64.319.92.599.28.28.453.546.598.92.11.281.24.705.275 1.485.039.843.047 1.096.047 3.231s-.008 2.389-.047 3.232c-.035.78-.166 1.203-.275 1.485a2.47 2.47 0 0 1-.599.919c-.28.28-.546.453-.92.598-.28.11-.704.24-1.485.276-.843.038-1.096.047-3.232.047s-2.39-.009-3.233-.047c-.78-.036-1.203-.166-1.485-.276a2.478 2.478 0 0 1-.92-.598 2.48 2.48 0 0 1-.6-.92c-.109-.281-.24-.705-.275-1.485-.038-.843-.046-1.096-.046-3.233 0-2.136.008-2.388.046-3.231.036-.78.166-1.204.276-1.486.145-.373.319-.64.599-.92.28-.28.546-.453.92-.598.282-.11.705-.24 1.485-.276.738-.034 1.024-.044 2.515-.045v.002zm4.988 1.328a.96.96 0 1 0 0 1.92.96.96 0 0 0 0-1.92zm-4.27 1.122a4.109 4.109 0 1 0 0 8.217 4.109 4.109 0 0 0 0-8.217zm0 1.441a2.667 2.667 0 1 1 0 5.334 2.667 2.667 0 0 1 0-5.334z"/>
    </svg>
    <svg xmlns="http://www.w3.org/2000/svg" width="30" height="30" fill="currentColor" class=" bi bi-youtube m-2" viewBox="0 0 16 16">
        <path d="M8.051 1.999h.089c.822.003 4.987.033 6.11.335a2.01 2.01 0 0 1 1.415 1.42c.101.38.172.883.22 1.402l.01.104.022.26.008.104c.065.914.073 1.77.074 1.957v.075c-.001.194-.01 1.108-.082 2.06l-.008.105-.009.104c-.05.572-.124 1.14-.235 1.558a2.007 2.007 0 0 1-1.415 1.42c-1.16.312-5.569.334-6.18.335h-.142c-.309 0-1.587-.006-2.927-.052l-.17-.006-.087-.004-.171-.007-.171-.007c-1.11-.049-2.167-.128-2.654-.26a2.007 2.007 0 0 1-1.415-1.419c-.111-.417-.185-.986-.235-1.558L.09 9.82l-.008-.104A31.4 31.4 0 0 1 0 7.68v-.123c.002-.215.01-.958.064-1.778l.007-.103.003-.052.008-.104.022-.26.01-.104c.048-.519.119-1.023.22-1.402a2.007 2.007 0 0 1 1.415-1.42c.487-.13 1.544-.21 2.654-.26l.17-.007.172-.006.086-.003.171-.007A99.788 99.788 0 0 1 7.858 2h.193zM6.4 5.209v4.818l4.157-2.408L6.4 5.209z"/>
    </svg>
    <h5>Campus:</h5>
    <p>454 Collins Street, Melbourne, VIC 3000</p>
    <p>Hybrid learning in Melbourne</p>
    <p>Remote learning Australia wide</p>
  </div>
  </footer>
</template>

<style>
  @media only screen and (min-width: 800px)
  {
    div#home h1{
      font-size: 70px;
    }
    div#home h4{
      font-size: 40px;
    }
    div#course{
      font-size: 23px;
    }
    #course #carouselExampleControls{
    margin:50px 150px;
    padding:20px;
    }

  }

  @media only screen and (max-width: 800px)
  {
    #course #carouselExampleControls{
    margin:30px 70px;
    padding:20px;
  }
  }

/*
  .carousel-control-prev-icon {
        background-image:url("data:image/svg+xml;charset=utf8,%3Csvg xmlns='http://www.w3.org/2000/svg' fill='black' viewBox='0 0 8 8'%3E%3Cpath d='M5.25 0l-4 4 4 4 1.5-1.5-2.5-2.5 2.5-2.5-1.5-1.5z'/%3E%3C/svg%3E");
    }
    .carousel-control-next-icon {
        background-image: url("data:image/svg+xml;charset=utf8,%3Csvg xmlns='http://www.w3.org/2000/svg' fill='black' viewBox='0 0 8 8'%3E%3Cpath d='M2.75 0l-1.5 1.5 2.5 2.5-2.5 2.5 1.5 1.5 4-4-4-4z'/%3E%3C/svg%3E");

    }*/


  #about img{
      width: 40%;
  }



  #course #carouselExampleControls{
    background-color: rgb(42, 38, 32);

    border: 1px solid rgb(42, 38, 32);
    border-radius: 15px;
    opacity: 0.8;
    color: white;
  }

  #enroll{
    border: 1px solid black;
    color: aliceblue;
  }

  div#home{
      font-family: "Times New Roman", Times, serif;
      background-image: url('../assets/coding.jpg');
      background-attachment:scroll;
      background-size: 110% 100%;
      color:rgb(250, 250, 250);
      padding-top: 15%;
      padding-bottom: 15%;
  }
  button
  {
    background-color: rgb(188, 9, 9);
    border: 1px solid white;
    border-radius: 10px;
    opacity: 0.7;
  }
  button:hover
  {
    border: rgb(188, 9, 9);
    opacity: 1;
  }

  div#about{
    margin-top: 20px;
    color: rgb(241, 241, 245);
  }

  div#about h3{
    color: rgb(188, 9, 9);
  }

  div#course{
    height: 550px;
    background-color: whitesmoke;;
    color: black;
    background-size: 100% 100%;
    background-image: url('../assets/class.png');
  }

  #contact, #logo{
    color:rgb(99, 101, 101);
  }

  #contact h2{
    color: rgb(145, 52, 52);
  }

</style>

<script>

export default {
  name: 'HomeView',
  data: function()
  {
    return{
      msg:[],
      account: false

    }
  },
  mounted()
  {
    if(localStorage.getItem("user-name"))
    {
      this.account = true;
    }
    fetch('http://localhost:3000/units')
    .then( response =>{
      return response.json( );
    })
    .then( data =>{
      this.msg=data;
    })
    .catch(error => {
      this.err=error
    });
  },

  methods:
  {
    logIn()
    {
      this.$router.replace({ name: "login" });
    },
    signUp()
    {
      this.$router.replace({ name: "signup" });
    },
    viewCourse(a){
      this.$router.replace({ name: a });
    }

  }
}
</script>
