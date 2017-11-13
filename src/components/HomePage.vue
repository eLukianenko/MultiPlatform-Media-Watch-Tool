<template>
    <div>
        <nav class="navbar navbar-default">
            <div class="container-fluid">
                <div class="collapse navbar-collapse">
                    <ul class="nav navbar-nav">
                        <li class="dropdown">
                            <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">ADD STREAMS <span class="caret"></span></a>
                            <toolbar class="toolbar dropdown-menu" @setStreamData="setStreamArray"></toolbar>
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
            <twitch v-if="stream.platform =='twitch'"
                    :channel="stream.url"
                    :width="streamWidth"
                    :height="streamHeight"
                    :chat="settings.chat"
            ></twitch>
        </div>
        <div v-for="stream in streamsArray" class="youtube">
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
                widthMin: 580,
                widthDefault: 780,
                heightMin: 440,
                heightDefault: 480,
                streamsArray: [],
                settings: {},
                showHello: true,
            }
        },
        computed: {
            /**
             * Stream width
             *
             * @returns {number}
             */
            streamWidth() {
                if (this.streamsArray.length > 4 && !this.settings.chat) {
                    return this.widthMin;
                } else return this.widthDefault;
            },
            /**
             * Stream height
             *
             * @returns {number}
             */
            streamHeight() {
                if (this.streamsArray.length > 4 && !this.settings.chat) {
                    return this.heightMin;
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
                $('[data-toggle="dropdown"]').parent().removeClass('open');
            },

            /**
             * Set stream array with data from toolbar component
             *
             * @returns {void}
             */
            setStreamArray(streamArray) {
                this.cleanHomePage();
                this.$nextTick(function () {
                    this.streamsArray = streamArray.streams;
                });
                for(let index in streamArray.settings) {
                    let key = streamArray.settings[index];
                    this.settings[key] = true;
                }
            }
        }
    }
</script>

<style scoped>
    h1 {
        color:darkslategray;
    }
    .title{
        padding-top: 15px;
        padding-bottom: 15px;
        padding-right: 130px;
        font-size: large;
    }
    .toolbar {
        width: 400px;
        background-color: lightblue;
        text-align: center;
    }
    img {
        width: 450px;
        height: 300px;
    }
    .youtube {
        margin-left: 9%;
    }
</style>