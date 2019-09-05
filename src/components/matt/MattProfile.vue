<template>
   <div>
     <header class="hero">
       <nav>
         <router-link v-bind:to="'./'"><img class="logo" src="./MattImages/TTAMLogoWhite.png"></router-link>
         <ul>
           <li><router-link to="./Matt">Home</router-link></li>
           <li>|</li>
           <li><router-link to="./MattOurDesigners">Our Designers</router-link></li>
         </ul>
       </nav>
     </header>

     <MattBio :userdata="userdata"/>
     <MattProjectList :projectdata="projectdata" :userdata="userdata" />
     <MattMyFooter />
   </div> 
   </template>


<script>
import MattBio from "./MattBio"
import MattMyFooter from "./MattMyFooter"
import MattProjectList from "./MattProjectList"

export default {
 name: "MattProfile",
 components: {
   MattBio,
   MattMyFooter,
   MattProjectList
 },

data: function() {
    return {
      userId: "",
      userdata: {}, 
    }
  }, 
  created: function() {
      this.getUserData();
      this.getProjectData();
  },
  methods: {
    getUserData() {
      if (this.$route.params.userId) {
       this.userId = this.$route.params.userId;
       this.$http
         .get(
           "https://behance-mock-api.glitch.me/api/users/" +
            this.userId
          )
          .then(function(data) {
          this.userdata = data.body;
        });
      }
     },
     getProjectData() {
        if (this.$route.params.userId) {
          this.userId = this.$route.params.userId;
          this.$http
            .get(
              "https://behance-mock-api.glitch.me/api/users/" +
              this.userId +
              "/projects"
            )
            .then(function(data) {
              this.projectdata = data.body;
            });
      }
    }
  }
}

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Lato');

.hero{
 background-image: url(./MattImages/ProjectImage2.jpg);
 height: 50vh;
 background-size: cover;
 background-position: center;
}

.container {
 margin: 0 auto;
 overflow: hidden;

}

nav {
 padding: 10px 50px
}

nav, ul {
 display: flex;
 justify-content: space-between;

}

li {
 list-style: none;
 padding: 25px 5px;
 color: white;
 font-size: 30px;
 font-family: 'Lato', sans-serif;
}

.logo {
 height: 80px;
 width: 55px;
}

.headerText {
 Padding: 300px;
 font-size: 100px;
 color: white
}

a {
  color: white
}

</style>

