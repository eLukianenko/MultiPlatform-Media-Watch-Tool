<template>
  <div id="twitch-embed"></div>
</template>

<script>
export default {
    name: 'TwitchStream',
    props: ['channel', 'width', 'height', 'chat'],
    mounted () {
      new Twitch.Embed('twitch-embed', {
          channel: this.channel,
          width: this.width,
          height: this.height,
          layout: this.chat? '':'video',
          chat: 'default'
      })
    }
}
</script>
