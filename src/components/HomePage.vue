<style>
  .toolbar{

  }
</style>
<template>
  <div>
    <toolbar class="toolbar"></toolbar>
    <div v-for="stream in streamsArray">
      <twitch
              :channel="stream.streamName"
              :width="streamWidth"
              :height="streamHeight"
              :autoplay="settings.autoplay"
              :muted="settings.muted"
              :theme="settings.theme"
              :chat="settings.chat"
      ></twitch>
    </div>
  </div>
</template>
<script>
    import TwitchStream from './TwitchStream'
    import Toolbar from './ToolBar'

export default {
    name: 'HomePage',
    components: {
        'twitch': TwitchStream,
        'toolbar': Toolbar
    },
    data() {
        return {
            widthMin: 340,
            widthDefault: 940,
            heightMin: 400,
            heightDefault: 480,
            streamsArray: [],
            settings:[]
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
            this.streamsArray = streamsArray;
        },
        setSettingsArray(settingsArray){
            this.settings = settingsArray;
        }
    }
}
</script>