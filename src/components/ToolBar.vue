<template>
  <div>
    <form>
      <H4>Stream urls</H4>
      <div class="input-group control-group after-add-more">
        <input type="url" class="form-control" placeholder="Stream url" v-model="streamsArray">
        <div class="input-group-btn">
          <button class="btn btn-success add-more" type="button" v-if="!addClicked" @click="addField"><span class="glyphicon glyphicon-plus"></span></button>
          <button class="btn btn-danger remove" type="button" v-if="addClicked" @click="removeField"><span class="glyphicon glyphicon-minus"></span></button>
        </div>
      </div>

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
            streamsArray: [],
            addClicked: false
        }
    },
    mounted(){
    },
    methods: {
        sendData() {
            console.log(this.streamsArray);
        },
        addField() {
            this.addClicked = true;
//            let html = $(".copy").html();
//            $(".after-add-more").after(html);
        },
        removeField() {
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
</style>

