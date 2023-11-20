<template>
    <div class="my-5">
    <v-card class="box col-md-8 col-10 mx-auto">
      <v-card-text class="text-justify m-2 m-md-5">
      <hr>
      <h3>COS10009 - Introduction to Programming</h3>
      <p class="text-red">Aims and Objectives:</p>
      <p>This unit of study aims to introduce students to structured procedural programming and design.</p>
      <p class="text-red">Students who successfully complete this unit will be able to:</p>
      <ol >
          <li>Apply code reading and debugging techniques to analyse, interpret, and describe the purpose of program code, and locate within this code errors in syntax, logic, style and/or good practice (K6, S1). </li>
          <li>Describe the principles of structured programming, and relate these to the syntactical elements of the programming language used and the way programs are developed (A2, S1).</li>
          <li>Construct small programs, using the programming languages covered, that include the use of arrays, functions and procedures, parameter passing with call by value and call by reference, custom data types, and pointers (K1, K2, K3, S2). </li>
          <li>Use modular and functional decomposition to break problems down functionally, represent the resulting structures diagrammatically, and implement these structures in code as functions and procedures (S3, A2, A4).</li>
      </ol>
      <p class="text-red">General Skills Outcome</p>
      <ul>
          <li> Problem solving</li>
          <li> Analysis skills</li>
          <li> Communication skills</li>
          <li>Ability to tackle unfamiliar problems</li>
          <li>Ability to work independently</li>
      </ul>
      <button @click="logIn" type="button" v-if="login==false" class="py-3 px-2 px-md-10 text-white">Log In to Enroll</button>
      <button @click="enroll" type="button" v-if="alreadyEnroll==false && login==true" class="py-3 px-2 px-md-10 text-white">Enroll Now</button>
      <h5 v-if="alreadyEnroll==true && login==true" class="text-success">You have already enrolled this course! Please check <a href="http://localhost:8080/user">My Enrollment</a> for more information!</h5>


      </v-card-text>
    </v-card>
    </div>

  </template>
  <style>
    .box{
        border-radius: 18px;
    }

  </style>
  <script>
  import axios from 'axios'

  export default { //json file location
  name: 'INTROView',
  data: function() {
    return {
      name: '',
      email: '',
      password:'',
      id: '',
      alreadyEnroll: false,
      login: false

    }
  },

  mounted()
  {this.name = localStorage.getItem("user-name");
    this.email = localStorage.getItem("user-email");
    this.password = localStorage.getItem("user-pwd");
    this.id =  localStorage.getItem("user-id");
    if(this.name)
    {
    this.login= true
    var self = this
    var readSQLApiURL = 'http://localhost:3000/enrollment'

    fetch(readSQLApiURL )
    .then( response =>{
    return response.json( );
    })
    .then( data =>{
    self.IDList = data.map(c => c.sid);
    self.codeList = data.map(c => c.courseCode);
    for (let index = 0; index < self.IDList.length; index++)
    {
      const element1 = self.IDList[index];
      const element2 = self.codeList[index];
      if(element1 == self.id)
      {
        if(element2 == 'COS10009')
        {
          this.alreadyEnroll = true;
        }
      }
    }
    })
  }
  },

  methods:{
    enroll(){
      let result = axios.post("http://localhost:3000/enrollment",
      {
        sid: this.id,
        courseCode: 'COS10009'
      });
      console.warn(result);

      this.alreadyEnroll = true;
    },
    logIn()
    {
      this.$router.push({ name: "login" });
    }
  }

  }
  </script>
