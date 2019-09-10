<template>
    <div>
      <header class="hero">
        <nav>
          <router-link v-bind:to="'./'"><img class="logo" src="./MattImages/TTAMLogo.png"></router-link>
          <ul>
            <li><router-link to="./Matt">Home</router-link></li>
            <li>|</li>
            <li><router-link to="./MattOurDesigners">Our Designers</router-link></li>
          </ul>
        </nav>
        <h1 class="headerText">TTAM Designs</h1>
      </header>
    </div>    
</template>


<script>

export default {
  name: "MattMyHeader",
  components: {
  }
};

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Just+Another+Hand');
@import url('https://fonts.googleapis.com/css?family=Lato');

.hero{
  background-image: url(./MattImages/blur-cellphone-close-up-196644.jpg);
  height: 100vh;
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
  Padding: 200px;
  font-size: 200px;
  color: black;
  font-family: 'Just Another Hand', cursive;
  font-weight: lighter
}

a {
  color: white
}
</style>