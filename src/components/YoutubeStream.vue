<template>
    <iframe :width="width"
            :height="height"
            :src="streamSRC"
    ></iframe>
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

<style scoped>
  iframe {
    float:right;
  }
</style>
