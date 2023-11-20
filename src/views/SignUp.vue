<template>
  <v-row>
  <v-col class="center">
    <v-card id="v" class="col-sm-6 col-md-4 mx-auto">
      <v-card-title>
        <h2>SIGN UP</h2>
      </v-card-title>

      <v-card-text>
      <v-form ref="form" v-model="valid" novalidate>
          <v-text-field v-model="uname" :rules="usernameRules" label="Username" required></v-text-field>
          <v-text-field v-model="mail" :rules="emailRules" label="Email" required></v-text-field>
          <v-text-field v-model="pwd" :rules="passwordRules" label="Password" type="password" required></v-text-field>

          <v-btn @click="signUp"   color="light-blue-lighten-3" class="mr-4">
              Sign Up
          </v-btn>

          <v-btn @click="reset"  color="warning" class="mr-4" >
              Reset
          </v-btn>
          <!--<p class="text-danger">{{msg}}</p>
          <ul v-for="m in Email" :key="m.id">
            <li><p>{{m}}</p></li>
          </ul>
          <p>{{user}}</p>-->
          <hr>
          <a href="http://localhost:8080/login">Already got account</a>
      </v-form>
      </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
  import axios from 'axios'
  export default {

      name:'SignUp',
      data: function()
      {
          return{
            user: localStorage.getItem("user-info"),
            uname:'',
            mail:'',
            pwd:'',
            msg:'',
            Email:[],
            valid: true,
            exist: false,
            usernameRules: [
            v => !!v || 'Name is required',
            v => (v && v.length <= 10) || 'Name must be less than 10 characters',
            ],
            passwordRules: [
            v => !!v || 'Password is required',
            v => (v && v.length >= 8) || 'Password must be more than 8 characters',
            ],
            emailRules: [
            v => !!v || 'E-mail is required',
            v => /[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,3}$/.test(v) || 'E-mail must be valid',
            ],
          }
      },
      mounted() {

        var self = this
        var readSQLApiURL = 'http://localhost:3000/users'

        fetch(readSQLApiURL )
        .then( response =>{
          return response.json( );
        })
        .then( data =>{
          self.Email = data.map(c => c.email);
        })
        .catch(error => {
          self.errorMessage = error;
        });

      },

      methods:{
        signUp()
        {
          for (let index = 0; index < this.Email.length; index++) {
              const element = this.Email[index];
              if (element==this.mail)
              {
                this.exist = true;
                this.msg = 'Email has already been used!'
                break;
              }
              else
              {
                this.msg='';
                this.exist = false;
              }
          }
          if (this.$refs.form.validate() && this.valid && !this.exist)
          {
            let result = axios.post("http://localhost:3000/users",
            {
              name: this.uname,
              email: this.mail,
              pwd: this.pwd
            });
            console.warn(result);
            this.$router.push({ name: "login" });
          }
        },
        reset()
        {
				this.$refs.form.reset()
        this.msg='';
        }
      }
  }
</script>

<style>
  #v{
      margin: 50px;
      border-radius: 18px;
  }
</style>
