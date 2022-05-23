<template>
  <table class="table">
    <thead>
      <ul style="padding-right: 40px">
        <li><strong>Código</strong></li>
        <li><strong>Nome</strong></li>
        <li><strong>Máximo</strong></li>
        <li><strong>Minimo</strong></li>
        <li><strong>Variação</strong></li>
      </ul>
    </thead>
    <tbody>
      <ul v-for="(item, key) in quotes" :key="key">
        <li>{{ key }}</li>
        <li>{{ item.name }}</li>
        <li>{{ item.high }}</li>
        <li>{{ item.low }}</li>
        <li>
          <span
            class="label label-rounded text-small"
            :class="{
              'label-error': item.pctChange < 0,
              'label-success': item.pctChange > 0,
            }"
          >
            {{ item.pctChange }}%
          </span>
        </li>
        <td>
          <a
            v-if="!listenQuotes.includes(key)"
            href="#"
            class="btn btn-primary btn-sm tooltip tooltip-left"
            data-tooltip="seguir"
            @click="$emit('listen', key)"
            ><i class="icon icon-plus"></i
          ></a>
          <a
            class="btn btn-error btn-sm tooltip tooltip-left"
            data-tooltip="Remover"
            v-else
            @click="$emit('unlisten', key)"
          >
            <i class="icon icon-minus"></i>
          </a>
        </td>
      </ul>
    </tbody>
  </table>
</template>

<script>
export default {
  props: {
    quotes: {
      type: Object,
      required: true,
    },
    listenQuotes: {
      type: Array,
      required: true,
    },
  },
  emits: ["listen", "unlisten"],
};
</script>

<style lang="scss" scoped>
ul {
  width: 100%;
  //   padding-right: 15px;
  display: flex;
  justify-content: space-between;

  li {
    display: flex;
    justify-content: center;
    align-items: center;

    width: 20%;
    list-style: none;
    border-bottom: 1px solid #d3d3d3;
    padding-bottom: 5px;
    span {
      height: 30px;
      width: 60px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  }
}
</style>
