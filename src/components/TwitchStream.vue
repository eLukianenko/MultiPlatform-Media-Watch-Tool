<template>
  <div id="twitch-embed"></div>
</template>
<script>
export default {
    name: 'TwitchStream',
    props: ['channel', 'width', 'height', 'autoplay', 'mute', 'chat'],
    mounted () {
      new Twitch.Embed('twitch-embed', {
          channel: this.channel,
          width: this.width,
          height: this.height,
          autoplay: this.autoplay,
          muted: this.mute,
          layout: this.chat? 'video-and-chat':'video'
      })
    }
}
</script>
