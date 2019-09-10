  <template>
    <div class="projectimages">
        <div v-for="project in projectdata.projects" v-bind:key="project.id">
            <img :src="project.covers['230']" :alt="project.name">
        </div>
    </div>

    
</template>


<script>


export default {
  name: "Designers",
  props: ["userdata", "projectdata"],
   watch: {
      projectId: function(val) {
        this.getProject(val);
      }
    }
}
</script>

<style scoped>

.projectimages {
    display: flex;
    justify-content: center;
    padding-bottom: 30px;
}

img {
 height: 300px;
 /* width: 35%; */
 margin: 20px; 
}

.stats {
  display: flex;
  justify-content: center;
  padding: 10px;
}
.stats h5 {
  padding: 10px;
}
</style>