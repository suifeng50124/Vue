<template>
  <div class="hello">
    <div>
      {{msg}}
    </div>
    <video id="my-video" ref="video" class="video-js vjs-default-skin" poster="http://vjs.zencdn.net/v/oceans.png" preload="auto">
      <source src="http://ivi.bupt.edu.cn/hls/cctv1.m3u8" type="application/x-mpegURL">
    </video>
    <div>
      <button @click="stop">播放</button>
      <button @click="createImage">截圖</button>
    </div>
  </div>
</template>

<script>
import videojs from "video.js";
import "videojs-contrib-hls";
// import 'video.js/dist/video-js.css'
export default {
  name: "HelloWorld",
  data() {
    return {
      msg: "Welcome to Your Vue.js",
      playStatus: false,
    };
  },
  created() {
    //  videojs(
    //   "my-video",
    //   {
    //     bigPlayButton: false,
    //     textTrackDisplay: false,
    //     posterImage: true,
    //     errorDisplay: false,
    //     // controlBar: true
    //   },
    //   function() {
    //     // this.play();
    //   }
    // );
  },
  mounted() {

    videojs(
      "my-video",
      {
        bigPlayButton: false,
        textTrackDisplay: false,
        posterImage: true,
        errorDisplay: false,
        // controlBar: true
      },
      function() {
        // this.play();
      }
    );
  },
  methods: {
    stop(){
      if (this.playStatus) {
        this.$refs.video.pause();
        this.playStatus = !this.playStatus
      }else{
        this.$refs.video.play();
        this.playStatus = !this.playStatus
      }
      
    },
    createImage() {
        // 生成截图
        const canvas = document.createElement('CANVAS');
        const size = {
          width: 200,
          height: 150
        };
        canvas.width = size.width;
        canvas.height = size.height;
        const ctx = canvas.getContext('2d');
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.drawImage(this.$refs.video, 0, 0, canvas.width, canvas.height);
        const imageURL = canvas.toDataURL('image/png');
        console.log(imageURL)
        return imageURL;
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#my-video {
  width: 100%;

}
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
