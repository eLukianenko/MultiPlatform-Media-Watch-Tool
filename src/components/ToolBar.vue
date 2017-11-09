<template>
  <div>
    <form>
      <H4>Stream urls</H4>
      <div v-for="stream in inputStreamsArray">
        <div class="input-group control-group">
          <input type="url" class="form-control" placeholder="Stream url" v-model="stream.value">
          <div class="input-group-btn">
            <button class="btn btn-danger remove" type="button"><span class="glyphicon glyphicon-minus"></span></button>
          </div>
        </div>
      </div>
      <button class="btn btn-success add-more" type="button" @click="addField"><span class="glyphicon glyphicon-plus"></span></button>
      <div class="form-check">
        <label class="form-check-label">
          <input type="checkbox" class="form-check-input">
          Enable stream autoplay(Twitch)
        </label>
        <label class="form-check-label">
          <input type="checkbox" class="form-check-input">
          Enable stream chat(Twitch)
        </label>
        <label class="form-check-label">
          <input type="checkbox" class="form-check-input">
          Mute stream(Twitch)
        </label>
      </div>
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
            streamsArray: []
        }
    },
    mounted(){
        $("body").on("click",".remove", function(){
            $(this).parents(".control-group").remove();
        });
    },
    methods: {
        sendData() {
            let vm = this;
            this.streamsArray = [];
            this.inputStreamsArray.forEach(function(item){
                let value = '';
                let platform = '';
                if(item.value.indexOf("youtube.com")+1) {
                    value = item.value.substr(item.value.lastIndexOf("=")+1);
                    platform = "youtube";
                }
                if(item.value.indexOf("twitch.tv")+1) {
                    value = item.value.substr(item.value.lastIndexOf("/")+1);
                    platform = "twitch";
                }

                vm.streamsArray.push({value: value, platform: platform});
            });
            this.$emit('sendStreamData', { data: this.streamsArray })
        },
        addField() {
            this.inputStreamsArray.push({ value: '' });
        }
    }
}
</script>
<style>
  .input-group{
    width: 90%;
    margin-left: 5%;
    margin-top: 5%;
  }
  .form-check {
    margin-top: 5%;
    text-align: left;
    margin-left: 5%;
  }
  form{
    margin: 2%;
  }
  .add-more {
    margin-top: 3%;
  }
</style>

