<template>
    <div>
        <nav class="navbar navbar-default">
            <div class="container-fluid">
                <div class="collapse navbar-collapse">
                    <ul class="nav navbar-nav">
                        <li class="dropdown" :class="toggleClass" @click.stop="toggle">
                            <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">ADD STREAMS <span class="caret"></span></a>
                            <toolbar @setStreamData="setStreamArray"></toolbar>
                        </li>
                    </ul>
                    <div class="title">MULTIPLATFORM</div>
                </div>
            </div>
        </nav>

        <div v-if="showHello">
            <img src="../assets/YouTubeTwitch.jpg">
            <h1>Welcome to Multiplatform stream view service!</h1>
        </div>
        <div v-for="stream in streamsArray">
            <twitch v-if="stream.platform == 'twitch'"
                    :channel="stream.url"
                    :width="streamWidth"
                    :height="streamHeight"
                    :chat="settings.chat"
            ></twitch>
        </div>
        <div v-for="stream in streamsArray" class="youtube">
            <youtube v-if="stream.platform == 'youtube'"
                     :channel="stream.url"
                     :width="streamWidth"
                     :height="streamHeight"
            ></youtube>
        </div>
    </div>
</template>

<script>
    import Twitch from './TwitchStream'
    import Youtube from './YoutubeStream'
    import Toolbar from './ToolBar'

    export default {
        name: 'HomePage',
        components: {
            Twitch,
            Youtube,
            Toolbar
        },
        data() {
            return {
                widthMin: 580,
                widthDefault: 780,
                heightMin: 440,
                heightDefault: 480,
                streamsArray: [],
                settings: {},
                showHello: true,
                show: false
            }
        },
        mounted() {
            document.addEventListener('click', () => this.show = false)
        },
        computed: {
            /**
             * Stream width
             *
             * @returns {number}
             */
            streamWidth() {
                return (this.streamsArray.length > 4 && !this.settings.chat)
                  ? this.widthMin
                  : this.widthDefault;
            },
            /**
             * Stream height
             *
             * @returns {number}
             */
            streamHeight() {
                return (this.streamsArray.length > 4 && !this.settings.chat)
                    ? this.heightMin
                    : this.heightDefault;
            },
            /**
             * Toggle class
             *
             * @returns {boolean}
            */
            toggleClass() {
                return {
                    open: this.show
                }
            }
        },
        methods: {
            /**
             * Toggle show/hide mehu
             *
             * @returns {void}
             */
            toggle() {
                this.show = !this.show;
            },

            /**
             * Set default settings
             *
             * @returns {void}
             */
            setDefaultSettings() {
                this.settings.chat = false;
            },

            /**
             * Clean home page from streams and set default settings
             *
             * @returns {void}
             */
            cleanHomePage() {
                this.showHello = false;
                this.streamsArray = [];
                this.setDefaultSettings();
                this.toggle();
            },

            /**
             * Set stream array with data from toolbar component
             *
             * @returns {void}
             */
            setStreamArray(streamArray) {
                this.cleanHomePage();
                this.$nextTick(() => this.streamsArray = streamArray.streams);

                streamArray.settings.forEach((item, i, arr) => this.settings[item] = true);
            }
        }
    }
</script>

<style scoped>
    h1 {
        color: darkslategray;
    }
    .title {
        padding-top: 15px;
        padding-bottom: 15px;
        padding-right: 130px;
        font-size: large;
    }
    img {
        width: 450px;
        height: 300px;
    }
    .youtube {
        margin-left: 9%;
    }
</style>
