<template>
    <div>
        <toolbar class="toolbar dropdown-menu" @setStreamData="setStreamArray"></toolbar>
        <div v-if="showHello">
            <img src="../assets/YouTubeTwitch.jpg">
            <h2>Welcome to Multiplatform stream view service!</h2>
            <h4>Please add stream urls in toolbar!</h4>
        </div>
        <button class="btn btn-primary add-streams dropdown-toggle" data-toggle="dropdown">
            ADD STREAMS <span class="caret"></span>
        </button>
        <div v-for="stream in streamsArray">
            <twitch v-if="stream.platform =='twitch'"
                    :channel="stream.url"
                    :width="streamWidth"
                    :height="streamHeight"
                    :autoplay="settings.autoplay"
                    :muted="settings.mute"
                    :chat="settings.chat"
            ></twitch>
            <youtube v-if="stream.platform =='youtube'"
                     :channel="stream.url"
                     :width="streamWidth"
                     :height="streamHeight"
            ></youtube>
        </div>
    </div>
</template>

<script>
    import TwitchStream from './TwitchStream'
    import YoutubeStream from './YoutubeStream'
    import Toolbar from './ToolBar'

    export default {
        name: 'HomePage',
        components: {
            'twitch': TwitchStream,
            'youtube': YoutubeStream,
            'toolbar': Toolbar
        },
        data() {
            return {
                widthMin: 340,
                widthDefault: 780,
                heightMin: 400,
                heightDefault: 480,
                streamsArray: [],
                settings: {},
                showHello: true,
                showToolbar: false
            }
        },
        computed: {
            /**
             * Stream width
             *
             * @returns {number}
             */
            streamWidth() {
                if (this.streamsArray.length > 4) {
//counting logic
                } else return this.widthDefault;
            },
            /**
             * Stream height
             *
             * @returns {number}
             */
            streamHeight() {
                if (this.streamsArray.length > 4) {
//counting logic
                } else return this.heightDefault;
            }
        },
        mounted() {
            $(document).on('click', '.dropdown-menu, .remove', function (e) {
                e.stopPropagation();
            });
        },
        methods: {
            /**
             * Set default settings
             *
             * @returns {void}
             */
            setDefaultSettings() {
                this.settings.autoplay = false;
                this.settings.chat = false;
                this.settings.mute = false;
            },

            /**
             * Set stream array with data from toolbar component
             *
             * @returns {void}
             */
            setStreamArray(streamArray) {
                this.showHello = false;
                this.showToolbar = false;
                this.cleanHomePage();

                for(let index in streamArray.settings) {
                    let key = streamArray.settings[index];
                    this.settings[key] = true;
                }
            },

            /**
             * Clean home page from streams and set default settings
             *
             * @returns {void}
             */
            cleanHomePage() {
                this.setDefaultSettings();
                this.streamsArray = [];
            }
        }
    }
</script>

<style>
    .toolbar {
        width: 300px;
        background-color: lightblue;
        top: 4.5%;
        text-align: center;
    }

    .add-streams {
        position: absolute;
        top: 1%;
        left: 2%;
    }

    img {
        width: 450px;
        height: 300px;
    }
</style>