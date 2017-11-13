<template>
    <div>
        <form>
            <H4>Streams <button class="btn btn-success add-more" type="button" @click="addField"><span
                    class="glyphicon glyphicon-plus"></span></button></H4>

            <div v-for="(stream, index) in inputStreamsArray">
                <div class="input-group control-group">
                    <input type="url" class="form-control" placeholder="Stream url" v-model="stream.url">
                    <div class="input-group-btn">
                        <button class="btn btn-danger remove" type="button" @click="inputStreamsArray.splice(index, 1)"><span
                                class="glyphicon glyphicon-minus"></span></button>
                    </div>
                </div>
            </div>

            <div class="form-check">
                <label class="form-check-label">
                    <input type="checkbox" class="form-check-input" v-model="settingsArray" value="chat">
                    Enable stream chat(Twitch)
                </label>
            </div>
            <button type="submit" class="btn btn-danger" @click="initiateInputFields">CLEAR</button>
            <button type="submit" class="btn btn-primary" @click="sendData">SHOW</button>
        </form>
    </div>
</template>

<script>
    export default {
        name: 'ToolBar',
        data() {
            return {
                inputStreamsArray: [],
                streamsArray: [],
                settingsArray: []
            }
        },
        mounted(){
            this.initiateInputFields()
        },
        methods: {
            /**
             * Send data to home page with streams
             */
            sendData() {
                let vm = this;
                this.streamsArray = [];

                this.inputStreamsArray.forEach(function (item) {
                    let url = '';
                    let platform = '';
                    let dataUrl = item.url;

                    if (dataUrl.indexOf("youtube.com") + 1) {
                        url = dataUrl.substr(dataUrl.lastIndexOf("=") + 1);
                        platform = "youtube";
                    }
                    if (dataUrl.indexOf("twitch.tv") + 1) {
                        url = dataUrl.substr(dataUrl.lastIndexOf("/") + 1);
                        platform = "twitch";
                    }

                    vm.streamsArray.push({url: url, platform: platform});
                });
                this.$emit('setStreamData', {streams: this.streamsArray, settings: this.settingsArray})
            },
            /**
             * Add new input field to form
             */
            addField() {
                this.inputStreamsArray.push({url: ''});
            },
            /**
             * Initiate input fields
             */
            initiateInputFields() {
                this.inputStreamsArray = [];
                for(let i=0; i<4; i++) {
                    this.addField();
                }
            }
        }
    }
</script>

<style>
    .input-group {
        width: 90%;
        margin-left: 5%;
        margin-top: 5%;
    }
    .form-check {
        margin-left: 5%;
        margin-top: 5%;
        text-align: left;
    }
    label {
        font-weight: 500;
        display: block;
    }
    form {
        margin: 2%;
    }
</style>

