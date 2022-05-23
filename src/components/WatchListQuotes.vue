<template>
  <ListQuotes
    :quotes="quotes"
    :listen-quotes="listenQuotes"
    @unlisten="onUnlisten"
  />
  <div class="mt-2 text-right">
    <cite class="text-small">
      Atualizará novamente em <b>{{ nextupdateTime }} segundos</b>
    </cite>
  </div>
</template>
<script>
import { reactive, ref, toRefs } from "vue";
import ListQuotes from "@/components/ListQuotes.vue";
import api from "@/services/api";

export default {
  components: { ListQuotes },

  setup(props, { emit }) {
    // const interval = ref(null);
    const quotes = ref({});
    const nextupdateTime = ref(30);

    const methods = reactive({
      onUnlisten(code) {
        emit("unlisten", code);
      },

      async refresh() {
        const { data } = await api.listen(props.listenQuotes);
        quotes.value = data;
      },
    });

    return {
      ...toRefs(methods),
      quotes,
      nextupdateTime,
    };
  },

  props: {
    listenQuotes: {
      type: Array,
      required: true,
    },
  },
  mounted() {
    this.refresh();
  },
};
</script>
