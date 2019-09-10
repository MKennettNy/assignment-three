  <template>
    <div>
        <div class="container" v-if="userdata.user">
          <img :src="userdata.user.images['115']">
          <h1 class="username">{{ userdata.user.display_name }}</h1>
          <p>{{ userdata.user.occupation }}</p>
        <div>
        <span>{{ userdata.user.city }}, </span>
        <span>{{ userdata.user.country }}</span>
        <div class='stats'>
          <h5>Followers: {{ userdata.user.stats.followers }}</h5>
          <h5>Following: {{ userdata.user.stats.following }}</h5>
          <h5>Views: {{ userdata.user.stats.views }}</h5>
        </div>
        </div>
        </div>
    </div>
</template>


<script>


export default {
  name: "Designers",
  props: ["userdata"],
   watch: {
     userdata: function(val) {
       this.userdata=val;
    }
  }
}
</script>

<style scoped>

img {
 height: 200px;
 /* width: 35%; */
 margin-top: 20px;
 border-radius: 50%
}

.stats {
  display: flex;
  justify-content: center;
  padding: 10px;
}
.stats h5 {
  padding: 30px 40px;
}

.username {
  padding: 30px;
}
</style>