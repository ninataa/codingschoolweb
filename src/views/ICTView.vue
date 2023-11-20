<template>
  <div class="my-5">
  <v-card class="box col-md-8 col-10 mx-auto">
    <v-card-text class="text-justify m-2 m-md-5">
    <hr>
    <h3>ICT10001 – Problem Solving with ICT</h3>
    <p class="text-red">Aims and Objectives:</p>
    <p>Every day we are faced with problems that require analytical thinking, creativity and resourcefulness to solve. This unit challenges students to explore different approaches to analysing and solving problems in an organisation framework. Students will develop the ability to apply analysis techniques to unfamiliar problems and present their investigation through the use of a wide range of innovative Information Communication Technologies [ICT], including prototyping, cloud-based tools, report writing and presentations. In addition, students are encouraged to reflect upon the learning taking place throughout the unit.</p>
    <p class="text-red">Students who successfully complete this unit will be able to:</p>
    <ol >
        <li>Identify and define problems in an organisational context.</li>
        <li>Select and apply various ICT tools and techniques to solve organisational problems.</li>
        <li>Build a solution to address an organisation problem.</li>
        <li> Evaluate the effectiveness and viability of an ICT solution from an organisational value perspective.</li>
        <li>Demonstrate working effectively in a team environment.</li>
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
name: 'ICTView',
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
  {
    this.name = localStorage.getItem("user-name");
    this.email = localStorage.getItem("user-email");
    this.password = localStorage.getItem("user-pwd");
    this.id =  localStorage.getItem("user-id");
    if(this.name)
    {
    this.login =  true
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
        if(element2 == 'ICT10001')
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
        courseCode: 'ICT10001'
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
