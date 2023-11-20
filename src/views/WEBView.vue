<template>
    <div class="my-5">
    <v-card class="box col-md-8 col-10 mx-auto">
      <v-card-text class="text-justify m-2 m-md-5">
      <hr>
      <h3>COS10005 – Web Development</h3>
      <p class="text-red">Aims and Objectives:</p>
      <p>To introduce the technology of the Internet and World Wide Web and to develop an understanding of the technologies associated with programming for the World Wide Web.</p>
      <p class="text-red">Students who successfully complete this unit will be able to:</p>
      <ol >
          <li>Develop web pages using HTML, JavaScript and CSS.</li>
          <li>Demonstrate an understanding of the key technologies of the World Wide Web.</li>
          <li>Describe the protocols of the World Wide Web.</li>
          <li>Design effective and user-friendly web pages using usability principles and style guides.</li>
          <li>Demonstrate an understanding of the history of the Internet and World Wide Web.</li>
      </ol>
      <p class="text-red">General Skills Outcome</p>
      <ul>
          <li> Problem solving</li>
          <li> Analysis skills</li>
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
  name: 'WEBView',
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
        if(element2 == 'COS10005')
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
        courseCode: 'COS10005'
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
