<template>
  <div class="">
    <div class="row">
      <div class="col-md-12 mb-5" v-if="createNew">
        <CreateVideo v-on:createdVideo="updatedVideos"/>
      </div>

      <div class="col-mb-5 text-center nicefont">
        <h4>
          Welcome to Youtube Rater
        </h4>
        <form @submit="createdNew()">
          <input class="btn-sm btn-primary mb-3 btn-center" id="createdNew" type="submit" value="Create new video">
        </form>
        <p v-bind:key="video.id" v-for="video in videos">
          Video:
          {{ video.title }}
          <br>
          Rating:
          {{ video.rating_average }}
          {{ video.comments_list }}
          <button v-on:click="videoDetail(video)" class="btn-sm btn-primary mt-2 mb-3">Details</button>
        </p>

      </div>

      <div class="col-md-6">
        <VideoDetails v-bind:videodetail="videodetail" v-on:updated="updatedVideos" v-on:deleted="updatedVideos"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import VideoDetails from "@/components/VideoDetails";
import CreateVideo from "@/components/CreateVideo";

export default {
  name: "ListVideos",
  components: {
    VideoDetails,
    CreateVideo,
  },
  data(){
    return {
      videos: [],
      videodetail: Object,
      createNew: "",
    }
  },
  methods: {
    getVideos(){
      axios.get("http://127.0.0.1:8000/api/videos/")
      .then(res => (this.videos = res.data))
      .catch(err => console.log(err));
      console.log(this.videos)
    },
    videoDetail(video){
      this.videodetail = video
      console.log(this.videodetail)
    },
    createdNew(){
      this.createNew = !this.createNew
    },
    updatedVideos(){
      setTimeout(() => {
         axios.get('http://127.0.0.1:8000/api/videos/')
        .then(res => (this.videos = res.data))
        .catch(err => (console.log(err)))
      }, 600);

    }
  },
  created() {
    this.getVideos()
    createNew: false;
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Slab:wght@500&display=swap');

.nicefont{
  font-size: 26px;
  font-family: 'Roboto Slab', serif;
}
</style>