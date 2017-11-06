<style>
  .toolbar{

  }
</style>
<template>
  <div>
    <toolbar class="toolbar"></toolbar>
    <div v-if="showHello">
      <img src="../assets/YouTubeTwitch.jpg" width="500px" height="300px">
      <h1>Welcome to Multiplatform stream view service!</h1>
      <h2>Please add stream url in toolbar and enjoy!</h2>
    </div>
    <div v-for="stream in streamsArray">
      <twitch v-if="stream.platform =='twitch'"
              :channel="stream.streamName"
              :width="streamWidth"
              :height="streamHeight"
              :autoplay="settings.autoplay"
              :muted="settings.muted"
              :theme="settings.theme"
              :chat="settings.chat"
      ></twitch>
      <youtube v-if="stream.platform =='youtube'"
               :channel="stream.streamName"
               :width="streamWidth"
               :height="streamHeight"></youtube>
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
            widthDefault: 940,
            heightMin: 400,
            heightDefault: 480,
            streamsArray: [],
            settings:[],
            showHello: true
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
            this.streamsArray = streamsArray;
        },
        setSettingsArray(settingsArray){
            this.settings = settingsArray;
        }
    }
}
</script>