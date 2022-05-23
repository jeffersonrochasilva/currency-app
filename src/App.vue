<template>
  <div class="conteiner grid-lg my-2 py-2">
    <div class="card mb-2" v-if="listenQuotes.length > 0">
      <div class="card-header">
        <div class="h4">Acompanhando</div>
      </div>
      <div class="card-body">
        <WatchListQuotes :listen-quotes="listenQuotes" @unlisten='onUnlisten'/>
      </div>
    </div>
    <div class="card">
      <div class="car-header">
        <div class="h4">todas as moedas</div>
      </div>
      <div class="card-body">
        <ListQuotes
          :quotes="quotes"
          :listen-quotes="listenQuotes"
          @listen="onListen"
          @unlisten="onUnlisten"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ListQuotes from "@/components/ListQuotes.vue";

import { reactive, toRefs } from "vue";
import api from "@/services/api";
import WatchListQuotes from "./components/WatchListQuotes.vue";

export default {
  components: { ListQuotes, WatchListQuotes },
  name: "App",
  setup() {
    const data = reactive({
      quotes: {},
      test: "",
      listenQuotes: [],
    });

    function onListen(code) {
      data.listenQuotes.push(code);
      console.log(data);
    }
    function onUnListen(code) {
      data.listenQuotes = data.listenQuotes.filter((item) => item !== code);
    }
    api.all().then((res) => {
      data.quotes = res.data;
    });


    return { ...toRefs(data), onListen, onUnListen };
  },


  
  //  Mounted(  () => {
  //     const response = await api.all();
  //     data.quotes = response.data;
  //     console.log("response", response);
  //   });


};
</script>

<style lang="scss" scoped>

.h4 {
  margin-left: 10%;
}
</style>
