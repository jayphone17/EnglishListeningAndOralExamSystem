<template>
  <div class="full-width">
    <v-row align="center">
      <img style="max-width: 300px" :src="state.downloadUrl" alt="请上传图片" />
      <v-btn @click="uploadAction" class="ml-5" color="green">上传图片</v-btn>
    </v-row>
  </div>
</template>

<script>
import { defineComponent, reactive, watch } from "@vue/composition-api";
import { downloadApiBase } from "../api/config";
import { upload } from "../utils/upload";

export default defineComponent({
  props: ["value"],
  setup(props, context) {
    const state = reactive({
      downloadUrl: `${downloadApiBase}${props.value}`,
    });
    const uploadAction = async () => {
      const value = await upload();
      context.emit("input", value);
      state.downloadUrl = `${downloadApiBase}${value}`;
    };
    watch(props, () => {
      state.downloadUrl = `${downloadApiBase}${props.value}`;
    });
    return {
      state,
      uploadAction,
    };
  },
});
</script>
