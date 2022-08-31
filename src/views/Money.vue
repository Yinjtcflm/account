<template>
  <Layout classPrefix="layout">
    <NumberPad :value.sync="record.amount" @submit="saveRecord" />
    <Types :value.sync="record.type" />
    <Notes
      fieldName="备注"
      placeholder="在这里输入备注"
      @update:value="onUpdateNotes"
    />
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
import recordListModel from "@/models/recordListModel";
import tagListModel from "@/models/recordListModel";

const recordList = recordListModel.fetch();
const tagList = tagListModel.fetch();

@Component({
  components: { NumberPad, Types, Tags, Notes },
})
export default class Money extends Vue {
  tags = tagList;
  recordList: RecordItem[] = recordList;
  record: RecordItem = { tags: [], type: "-", notes: "", amount: 0 };

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
    const record2: RecordItem = recordListModel.clone(this.record);
    record2.time = new Date();
    this.recordList.push(record2);
    console.log(record2);
  }
  @Watch("recordList")
  onRecordListChange() {
    recordListModel.save(this.recordList);
  }
}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>

