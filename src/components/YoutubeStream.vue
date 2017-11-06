<template>
  <div>
    <iframe :width="width"
            :height="height"
            :src="streamSRC"
            frameborder="0"
            allowfullscreen></iframe>
  </div>
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
