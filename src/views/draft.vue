signUp: function()
      {

          // Read the contents of the JSON file

          var self = this;

          const requestOptions = {
          method: 'POST',
          headers: {
          'Content-Type': 'application/json; charset=UTF-8'
          },
          body: JSON.stringify({
            name: this.uname,
            email: this.mail,
            pwd: this.pwd
          })

          };

          fetch('http://localhost:3000/post', requestOptions)
          .then( response =>{
          //turning the response into the usable data
          return response.json();
          })
          .then( data => {
          //This is the data you wanted to get from url
          self.msg = data;
          })
          .catch(error => {
          self.msg = 'There was an error!' + error;
          });
      }