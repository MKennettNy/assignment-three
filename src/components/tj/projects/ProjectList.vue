<template>
  <div>
    <div id="tabs" class="container">
  
      <div class="tabs">
        <a v-on:click="activetab=1" v-bind:class="[ activetab === 1 ? 'active' : '' ]">Projects</a>
        <a v-on:click="activetab=2" v-bind:class="[ activetab === 2 ? 'active' : '' ]">About Me</a>
      </div>
  
      <div class="content">
        <div v-if="activetab === 1" class="tabcontent">
          <div class="container">
            <div class="row">
              <div class="col-sm img-border" v-for="project in projectdata.projects" v-bind:key="project.id">
                <!-- <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12"> -->
                <div data-toggle="modal" data-target="#exampleModal" class="hovereffect">
                  <img class="img-responsive" :src="project.covers['230']" :alt="project.name">
                  <div data-toggle="modal" data-target="#exampleModal" class="overlay" v-on:click="projectIdChanged(project.id)">
                    <h5>{{ project.name }}</h5>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div v-if="activetab === 2" class="tabcontent">
          <div class="row about-me">
            <div class="col-8">
              <img class="user-icon" v-if="userdata.user.images['138']" :src="userdata.user.images['138']">
            </div>
            <div class="col-4">
              <h4>About</h4>
              <p>{{ userdata.user.display_name }}</p>
  
              <h4>Fields</h4>
              <p>
              <span>{{ userdata.user.fields['0'] }}, </span>
              <span>{{ userdata.user.fields['1'] }}, </span>
              <span>{{ userdata.user.fields['2'] }} </span>
              <span>{{ userdata.user.fields['3'] }} </span>
              </p>
  
              <h4>Socials</h4>
              <!-- <p>{{ userdata.user.social_links }}</p> -->
              <!-- <p>{{ userdata.user.social_links.url['0'] }}</p> -->
            </div>
          </div>
  
        </div>
      </div>
  
    </div>
  
    <ProjectModal :projectId="projectId" :userdata="userdata" />
  
  </div>
</template>

<script>
  import ProjectModal from "./ProjectModal";
  import $ from "jquery";
  
  export default {
    name: "ProjectList",
    // el: "#tabs",
    props: ["projectdata", "userdata"],
    data: function() {
      return {
        projectId: "",
        activetab: 1
      }
    },
    methods: {
      mouseOver: function() {
        this.active = !this.active;
        this.getFields();
      },
      projectIdChanged: function(projectId) {
        //  console.log("Change")
        this.projectId = projectId;
      },
      getFields: function() {
        let that = this;
        let test = this.projectdata.project.modules;
        that.images = [];
        $.each(test, function(i, image) {
          that.images.push(image.src);
        });
      }
    },
    components: {
      ProjectModal
    },
    watch: {
      projectId: function(val) {
        this.getProject(val);
      }
    }
  };
</script>


<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Merriweather|Montserrat:300,300i,400,600');
  .router-link-active {
    font-weight: 400;
  }
  
  .container {
    margin-top: 70px;
  }
  
  .user-icon {
    border-radius: 10px;
    width: 200px;
  }
  
  .img-border img {
    border-radius: 10px;
  }
  
  .website {
    text-decoration: underline;
  }
  
  .stats div {
    padding: 0;
  }
  
  .stats p {
    margin-bottom: 0;
  }
  
  .about-me {
    padding-top: 50px;
  }
  
  .col-4 {
    text-align: left;
  }
  
  /*
                              * https://imgur.com/a/5nDMmmB  Link to Image
                              */
  
  /* .landing {
    background-image: url("https://imgur.com/clOcGTs.jpg");
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    height: 25vh;
  }
   */
  .logo-img {
    height: 60px;
  }
  
  .navbar {
    background-color: transparent !important;
    color: #ffffff;
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    z-index: 2;
  }
  
  
  /* RESET */
  
  
  /* * {
                      box-sizing: border-box;
                      margin: 0;
                      padding: 0;
                    } */
  
  .container {
    max-width: 620px;
    min-width: 420px;
    margin: 40px auto;
    font-size: 0.9em;
    color: #888;
  }
  
  
  /* Style the tabs */
  
  .tabs {
    overflow: hidden;
    margin-left: 20px;
    margin-bottom: -2px;
  }
  
  .tabs ul {
    list-style-type: none;
    margin-left: 20px;
  }
  
  .tabs a {
    /* float: left; */
    cursor: pointer;
    padding: 12px 24px;
    transition: background-color 0.2s;
    /* border: 1px solid #ccc; */
    border-right: none;
    background-color: #f1f1f1;
    /* border-radius: 10px 10px 0 0; */
    font-weight: bold;
  }
  
  
  /* .tabs a:last-child {
              border-right: 1px solid #ccc;
            } */
  
  
  /* Change background color of tabs on hover */
  
  .tabs a:hover {
    background-color: #aaa;
    color: #fff;
  }
  
  
  /* Styling for active tab */
  
  .tabs a.active {
    background-color: #fff;
    color: #484848;
    border-bottom: 2px solid #fff;
    cursor: default;
  }
  
  
  /* Style the tab content */
  
  
  /* .tabcontent {
                        padding: 30px;
                        border: 1px solid #ccc;
                        border-radius: 10px;
                      box-shadow: 3px 3px 6px #e1e1e1
                    } */
  
  .hovereffect {
    width: 100%;
    height: 100%;
    float: left;
    border-radius: 20px;
    overflow: hidden;
    position: relative;
    text-align: center;
    cursor: default;
    background: #333;
  }
  
  .hovereffect .overlay {
    width: 100%;
    height: 100%;
    border-radius: 20px;
    position: absolute;
    overflow: hidden;
    top: 0;
    left: 0;
    padding: 50px 20px;
    cursor: pointer;
  }
  
  .overlay h5 {
    color: #fff;
    font-family: 'Montserrat', sans-serif;
    font-weight: 600;
  }
  
  .hovereffect img {
    display: block;
    position: relative;
    border-radius: 20px;
    max-width: none;
    width: calc(100% + 20px);
    -webkit-transition: opacity 0.35s, -webkit-transform 0.35s;
    transition: opacity 0.35s, transform 0.35s;
    -webkit-transform: translate3d(-10px, 0, 0);
    transform: translate3d(-10px, 0, 0);
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
  }
  
  .hovereffect:hover img {
    opacity: 0.4;
    filter: alpha(opacity=40);
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
  
  .hovereffect h2 {
    text-transform: uppercase;
    color: #fff;
    text-align: center;
    position: relative;
    font-size: 17px;
    overflow: hidden;
    padding: 0.5em 0;
    background-color: transparent;
  }
  
  .hovereffect h2:after {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 2px;
    background: #fff;
    content: '';
    -webkit-transition: -webkit-transform 0.35s;
    transition: transform 0.35s;
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
  }
  
  .hovereffect:hover h2:after {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
  
  .hovereffect a,
  .hovereffect p {
    color: #FFF;
    opacity: 0;
    filter: alpha(opacity=0);
    -webkit-transition: opacity 0.35s, -webkit-transform 0.35s;
    transition: opacity 0.35s, transform 0.35s;
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
  }
  
  .hovereffect:hover a,
  .hovereffect:hover p {
    opacity: 1;
    filter: alpha(opacity=100);
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }
</style>