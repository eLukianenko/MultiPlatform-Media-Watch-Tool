<template>
  <div>
    <form>
      <H4>Stream urls</H4>
      <div class="cont">
        <div class="input-group control-group after-add-more">
          <input type="url" class="form-control" placeholder="Stream url" v-model="streamsArray">
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
            console.log(this.streamsArray);
        },
        addField() {
            let html = $(".cont").last().clone(true);
            $(html).insertBefore(".add-more");
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

