<template>
    <div class="my-5">
    <v-card class="box col-md-8 col-10 mx-auto">
        <v-card-text class="text-justify m-2 m-md-5">
        <hr>
        <h3>INF10002 – Database Analysis and Design</h3>
        <p class="text-red">Aims and Objectives:</p>
        <p >Digital data is central to the modern economy. Transactions, managerial decisions, and strategy development rely on data. Databases are the tool used to create, store, organise, and disseminate data. This unit delivers the fundamental principles needed to effectively design and use databases. It seeks to unpack the notion of data, and introduce contemporary tools and techniques for storing, retrieving, exploiting, and visualising data. Emphasis is given to understanding data modelling and design approaches, and the emerging opportunities afforded by big data, social media, data analytics, and unstructured data. Both commercial and open-source database management tools are focused upon.</p>
        <p class="text-red">Students who successfully complete this unit will be able to:</p>
        <ol >
            <li> Define and explain fundamental data and database concepts including tables, relations, keys, queries, transactions, and structured, semi-structured, unstructured data</li>
            <li>Create, store, retrieve, exploit, and visualise data using modern database tools, functions, and techniques</li>
            <li>Understand and apply conventional data modelling techniques to solve practical database design problems</li>
            <li>Explain the impact of big data and modern data analytics tools in the design, use, and management of database systems.</li>
        </ol>
        <p class="text-red">General Skills Outcome</p>
        <ul>
            <li>Teamwork skills</li>
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
  name: 'INFView',
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
        if(element2 == 'INF10002')
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
        courseCode: 'INF10002'
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
