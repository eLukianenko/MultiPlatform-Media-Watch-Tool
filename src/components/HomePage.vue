<style>
  .toolbar{

  }
</style>
<template>
  <div>
    <toolbar class="toolbar"></toolbar>
    <twitch :channel="streamName" :width="streamWidth" :height="streamHeight"></twitch>
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
            streamName: 'godhunt',
            streamsArray: []
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
        }
    }
}
</script>