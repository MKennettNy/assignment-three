<template>
  <!-- Modal -->
  <div
    class='modal fade'
    id='exampleModal'
    tabindex='-1'
    role='dialog'
    aria-labelledby='exampleModalLabel'
    aria-hidden='true'
  >
    <div class='modal-dialog' role='document'>
      <div class='modal-content'>
        <div class='modal-body'>
          <button type='button' class='close' data-dismiss='modal' aria-label='Close'>
            <span aria-hidden='true'>&times;</span>
          </button>
          <div v-if='projectdata.project'>
            <h1 class='modal-title'>{{projectdata.project.name}}</h1>
            <ul class='modal-fields' v-for='field in fields' :key='field'>
              <li>{{field}}</li>
            </ul>

            <img v-for='image in images' :key='image' v-bind:src='image' class='modal-image'>
            <div class='row project-stats'>
              <div class='col-sm'>
                <h2>
                  <i class='fas fa-eye'></i>
                  {{projectdata.project.stats.views}}
                </h2>
              </div>
              <div class='col-sm'>
                <h2>
                  <i class='fas fa-thumbs-up'></i>
                  {{projectdata.project.stats.appreciations}}
                </h2>
              </div>
              <div class='col-sm'>
                <h2>
                  <i class='fas fa-comment-alt'></i>
                  {{projectdata.project.stats.comments}}
                </h2>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template> 

<script>
// To get around $ reference error
import $ from 'jquery';

export default {
  name: 'AshModal',
  props: ['projectId'],
  data() {
    return {
      projectdata: {},
      images: [],
      fields: []
    };
  },
  methods: {
    // Get images from array
    getImages: function() {
      let that = this;
      let test = this.projectdata.project.modules;
      that.images = [];
      $.each(test, function(i, image) {
        that.images.push(image.src);
      });
    },
    // Get fields from array
    getFields: function() {
      let that = this;
      let test = this.projectdata.project.fields;
      that.fields = [];
      $.each(test, function(i, field) {
        that.fields.push(field);
      });
    },
    getProject: function(projectId) {
      if (projectId) {
        this.$http
          .get('https://behance-mock-api.glitch.me/api/projects/' + projectId)
          .then(function(projectdata) {
            this.projectdata = projectdata.body;
            this.getImages();
            this.getFields();
          });
      }
    }
  },
  watch: {
    projectId: function(val) {
      this.getProject(val);
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=Libre+Baskerville|Montserrat');

.project-stats {
  width: 70%;
  margin: 0 auto;
}
.project-stats h2 {
  font-size: 15px;
  color: #222;
  margin-top: 20px;
  margin-bottom: 20px;
  font-family: 'Montserrat', sans-serif;
}
.project-stats i {
  padding: 10px;
}
.modal-image {
  max-width: 95%;
  margin-bottom: 20px;
  box-shadow: 4px 4px 7px lightgrey;
}
ul {
  list-style-type: none;
  display: inline-block;
  font-family: 'Montserrat', sans-serif;
  font-size: 15px;
}
.modal-title {
  font-family: 'Libre Baskerville', serif;
  font-size: 35px;
  color: #5b736a;
  margin-bottom: 20px;
  margin-top: 30px;
}
.modal-fields {
  margin-bottom: 40px;
  font-size: 15px;
}
.modal-dialog {
  max-width: 850px;
}
</style>
