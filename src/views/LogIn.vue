<template>
    <v-row>
    <v-col class="center">
        <v-card id="box" class="col-sm-6 col-md-4 mx-auto">
        <v-card-title>
          <h2>Log In</h2>
        </v-card-title>
                <v-card-text>
                <v-form ref="form" v-model="valid" novalidate>
                    <v-text-field v-model="uname" :rules="usernameRules" label="Username" required></v-text-field>
                    <v-text-field v-model="pwd" :rules="passwordRules" label="Password" type="password" required></v-text-field>

                    <v-btn v-on:click="logIn"   color="light-blue-lighten-3" class="mr-4">
                        Log In
                    </v-btn>

                    <v-btn v-on:click="reset" color="warning" class="mr-4" >
                        Reset
                    </v-btn>
                    <br>
                    <p class="text-danger">{{ msg }}</p>

                </v-form>
                <hr>
                <a href="http://localhost:8080/signup">Haven't sign up yet?</a>
                </v-card-text>
            </v-card>
        </v-col>
    </v-row>
  </template>

  <script>
    export default {

        name:'LogIn',
        data: function()
        {
            return{
                uname:'',
                mail:'',
                pwd:'',
                msg:'',
                nameList:'',
                pwdList:'',
                idList:'',
                valid:'',
                usernameRules: [
                v => !!v || 'Name is required',
                v => (v && v.length <= 10) || 'Name must be less than 10 characters',
                ],
                passwordRules: [
                v => !!v || 'Password is required',
                v => (v && v.length >= 8) || 'Password must be more than 8 characters',
                ]
            }
        },

        mounted() {
        if(localStorage.getItem("user-name"))
        {
            this.$router.push({ name: "user" });
        }
        else
        {
            var self = this
            var readSQLApiURL = 'http://localhost:3000/users'

            fetch(readSQLApiURL )
            .then( response =>{
            return response.json( );
            })
            .then( data =>{
            self.nameList = data.map(c => c.name);
            self.pwdList = data.map(c => c.pwd);
            self.mailList = data.map(c => c.email);
            self.idList = data.map(c => c.id);
            })
            .catch(error => {
            self.errorMessage = error;
            });
        }


      },

        methods:
        {
            logIn()
            {
                if (this.$refs.form.validate() && this.valid)
                {
                    if(this.nameList.length>0)
                    {
                        for (let index = 0; index < this.nameList.length; index++)
                        {
                        if(this.uname == this.nameList[index] && this.pwd == this.pwdList[index])
                        {
                            this.msg = "Log in successfully!";
                            this.$router.go({
                            path: "/",
                            force: true
                            });
                            localStorage.setItem("user-name", this.uname);
                            localStorage.setItem("user-pwd", this.pwd);
                            localStorage.setItem("user-email", this.mailList[index]);
                            localStorage.setItem("user-id", this.idList[index]);
                            break;
                        }
                        this.msg="Incorrect username or password!";
                        }
                    }
                    else
                    {
                        this.msg="Incorrect username or password!";
                    }

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
  #box{
      margin: 50px;
      border-radius: 18px;
  }
  </style>
