import Layout from '@/components/Layout.vue';
<template>
  <Layout classPrefix="layout">
    <NumberPad :value.sync="record.amount" @submit="saveRecord" />
    <Types :value.sync="record.type" />
    <Notes @update:value="onUpdateNotes" />
    <Tags :dataSource.sync="tags" @update:value="onUpdateTags" />
  </Layout>
</template>

<script lang="ts">
import Vue from "vue";
import NumberPad from "@/components/Money/NumberPad.vue";
import Types from "@/components/Money/Types.vue";
import Tags from "@/components/Money/Tags.vue";
import Notes from "@/components/Money/Notes.vue";
import { Component, Watch } from "vue-property-decorator";

const recordList = JSON.parse(
  window.localStorage.getItem("recordList") || "[]"
);
type Record = {
  tags: string[];
  type: string;
  notes: string;
  amount: number;
  time?: Date;
};

@Component({
  components: { NumberPad, Types, Tags, Notes },
})
export default class Money extends Vue {
  tags = ["衣", "食", "住", "行", "旅游"];
  recordList: Record[] = recordList;
  record: Record = { tags: [], type: "-", notes: "", amount: 0 };

  onUpdateTags(value: string[]) {
    this.record.tags = value;
  }
  onUpdateNotes(value: string) {
    this.record.notes = value;
  }
  onUpdateAmount(value: string) {
    this.record.amount = parseFloat(value);
  }
  saveRecord() {
    const record2: Record = JSON.parse(JSON.stringify(this.record));
    record2.time = new Date();
    this.recordList.push(record2);
    console.log(record2);
  }
  @Watch("recordList")
  onRecordListChange() {
    window.localStorage.setItem("recordList", JSON.stringify(this.recordList));
  }
}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>

