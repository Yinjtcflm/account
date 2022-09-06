<template>
  <Layout>
    <Tabs classPrefix="type" :dataSource="typeList" :value.sync="type" />
    <Tabs
      classPrefix="interval"
      :dataSource="intervalList"
      :value.sync="interval"
    />
  </Layout>
</template>

<style scoped lang="scss">
::v-deep .type-tabs-item {
  background: white;
  &.selected {
    background: #c4c4c4;
    &::after {
      display: none;
    }
  }
}
</style>
  
  <script lang="ts">
import Types from "../components/Money/Types.vue";
import Vue from "vue";
import { Component } from "vue-property-decorator";
import Tabs from "@/components/Tabs.vue";
@Component({
  components: { Tabs, Types },
})
export default class Statistics extends Vue {
  type = "-";
  interval = "day";
  typeList = [
    { text: "支出", value: "-" },
    { text: "收入", value: "+" },
  ];
  intervalList = [
    { text: "按天", value: "day" },
    { text: "按月", value: "month" },
    { text: "按年", value: "year" },
  ];
}
</script>
