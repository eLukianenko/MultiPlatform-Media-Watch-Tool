<template>
  <div id="twitch-embed" class="channel"></div>
</template>
<script>
export default {
    name: 'TwitchStream',
    props: ['channel', 'width', 'height', 'autoplay', 'muted', 'chat'],
    mounted () {
      new Twitch.Embed('twitch-embed', {
          channel: this.channel,
          width: this.width,
          height: this.height,
          autoplay: this.autoplay,
          muted: this.muted,
          layout: this.chat? 'video-and-chat':'video'
      })
    }
}
</script>
