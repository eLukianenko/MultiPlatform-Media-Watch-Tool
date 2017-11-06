<template>
  <div>
    <twitch :channel="streamName" :width="streamWidth" :height="streamHeight"></twitch>
  </div>
</template>
<script>
    import TwitchStream from './TwitchStream'

export default {
    name: 'HomePage',
    components: {
        'twitch': TwitchStream
    },
    data() {
        return {
            streamWidth: 854,
            streamHeight: 480,
            streamName: 'godhunt'
        }
    }
}
</script>
