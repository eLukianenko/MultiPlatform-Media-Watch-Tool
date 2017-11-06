<template>
  <div id="twitch-embed" class="channel"></div>
</template>
<script>
export default {
    name: 'TwitchStream',
    props: ['channel', 'width', 'height'],
    mounted () {
      new Twitch.Embed('twitch-embed', {
          width: this.width,
          height: this.height,
          channel: this.channel,
          layout: 'video',
          muted: true,
      })
    }
}
</script>
