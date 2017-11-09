<template>
  <div>
    <transition name="slide-fade">
      <toolbar class="toolbar" v-show="showToolbar" @sendStreamData="setStreamsArray"></toolbar>
    </transition>
    <div v-if="showHello">
      <img src="../assets/YouTubeTwitch.jpg">
      <h2>Welcome to Multiplatform stream view service!</h2>
      <h4>Please add stream urls in toolbar and enjoy!</h4>
    </div>
    <button @click="showToolbar = !showToolbar" class="btn btn-danger add-streams">
      ADD STREAMS
    </button>
    <div v-for="stream in streamsArray">
      <twitch v-if="stream.platform =='twitch'"
              :channel="stream.value"
              :width="streamWidth"
              :height="streamHeight"
              :autoplay="settings.autoplay"
              :muted="settings.muted"
              :chat="settings.chat"
              class="stream"
      ></twitch>
      <youtube v-if="stream.platform =='youtube'"
               :channel="stream.value"
               :width="streamWidth"
               :height="streamHeight"
      ></youtube>
    </div>
  </div>
</template>
<script>
    import TwitchStream from './TwitchStream'
    import YoutubeStream from './YoutubeStream'
    import Toolbar from './ToolBar'

export default {
    name: 'HomePage',
    components: {
        'twitch': TwitchStream,
        'youtube': YoutubeStream,
        'toolbar': Toolbar
    },
    data() {
        return {
            widthMin: 340,
            widthDefault: 780,
            heightMin: 400,
            heightDefault: 480,
            streamsArray: [],
            settings:[{autoplay:1},{muted:1}, {chat:true}],
            showHello: true,
            showToolbar: false
        }
    },
    computed: {
        streamWidth() {
            if(this.streamsArray.length>4) {
//counting logic
            } else return this.widthDefault;
        },
        streamHeight() {
            if(this.streamsArray.length>4) {
//counting logic
            } else return this.heightDefault;
        }
    },
    methods: {
        setStreamsArray(streamsArray){
            this.showHello = false;
            this.showToolbar = false;
            this.streamsArray = streamsArray.data;
        },
        setSettingsArray(settingsArray){
            this.settings = settingsArray;
        }
    }
}
</script>
<style>
  .toolbar{
    width: 300px;
    background-color: beige;
    position: absolute;
  }
  .add-streams{
    position: absolute;
    top:1%;
    left:2%;
  }
  img{
    width: 450px;
    height: 300px;
  }
  .stream {
    float: left;
  }
  .slide-fade-enter-active {
    transition: all .3s ease;
  }
  .slide-fade-leave-active {
    transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .slide-fade-enter, .slide-fade-leave-to{
    transform: translateX(10px);
    opacity: 0;
  }
</style>