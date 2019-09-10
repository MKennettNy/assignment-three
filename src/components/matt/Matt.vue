git<template>
    <div>
      <MattMyHeader />
      <MattFeaturedDesigners v-bind:users="users"/>
      <MattMyFooter />
    </div>  
</template>


<script>
import MattFeaturedDesigners from "./MattFeaturedDesigners"
import MattMyHeader from "./MattMyHeader"
import MattMyFooter from "./MattMyFooter"

export default {
  name: "Matt",
  components: {
    MattFeaturedDesigners,
    MattMyHeader,
    MattMyFooter
  },
    props: ['users'],
    data: function() {
    return {
      user: []
    }
  },
    created: function() { 
    this.$http
        .get("https://behance-mock-api.glitch.me/api/users") 
        .then(function(data) {
          this.users = data.body.users;
        });
    },
    methods: { 
    navigateTo: function(userId) {
      this.$router.push({ name: "Profile", params: { userId: userId } });
      }
    }
};

</script>

<style scoped>

</style>