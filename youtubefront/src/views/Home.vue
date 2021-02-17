<template>
  <div class="home">
<!--    <img alt="Vue logo" src="../assets/logo.png">-->
    <ListVideos msg="Welcome to Youtube Rater"/>
  </div>
</template>

<script>
// @ is an alias to /src
import ListVideos from "@/components/ListVideos";

export default {
  name: 'Home',
  components: {
    ListVideos
  }
}
</script>
