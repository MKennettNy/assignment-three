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
  <MattDesigners v-bind:users="users"/>   
  <MattMyFooter />
</div>
  


</template>

<script>
// import MyHeader from "./MyHeader"
import MattMyFooter from "./MattMyFooter"
import MattDesigners from "./MattDesigners"



export default {
  name: "OurDesigners",
  components: {
    // MyHeader,
    MattMyFooter,
    MattDesigners
  },
  data: function() {
    return {
      users: []
    }
  },
    created: function() { 
        this.$http
        .get("https://behance-mock-api.glitch.me/api/users") 
        .then(function(data) {
          this.users = data.body.users;
        });
    }
}


</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Lato');


.hero{
  background-image: url(./MattImages/ProjectImage3.jpg);
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
  font-weight: lighter
}

.logo {
  height: 80px;
  width: 55px;
  color: white;
}

.headerText {
  Padding: 200px;
  font-size: 200px;
  color: white;
  font-family: 'Just Another Hand', cursive;
  font-weight: lighter
}

a {
  color: white;
  
}

</style>