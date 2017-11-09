<template>
    <iframe :width="width"
            :height="height"
            :src="streamSRC"
            frameborder="0"
            allowfullscreen></iframe>
</template>
<script>
export default {
    name: 'TwitchStream',
    props: ['channel', 'width', 'height'],
    computed: {
        streamSRC() {
            return "https://youtube.com/embed/" + this.channel;
        }
    }
}
</script>
<style scoped="">
  iframe {
    float:right;
  }

  .clear {
    clear:both;
  }
</style>
