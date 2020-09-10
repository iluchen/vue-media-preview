<template>
  <div id="app">
    <div
      @click="clickUrl('https://ymr-test.oss-cn-hangzhou.aliyuncs.com/test-image/de5df880-2dbb-4607-9e1d-9bd77233d20d.jpg')"
    >{{imgUrl}}</div>
    <div
      @click="clickUrl('https://ymr-test.oss-cn-hangzhou.aliyuncs.com/douyin/a17d2103-4abd-4c46-bc13-044530667746.mp4')"
    >https://ymr-test.oss-cn-hangzhou.aliyuncs.com/douyin/a17d2103-4abd-4c46-bc13-044530667746.mp4</div>
    <div
      @click="clickUrl('https://ymr-test.oss-cn-hangzhou.aliyuncs.com/testfile/e04cc608-5842-48fb-929d-276d94ec1918.docx')"
    >https://ymr-test.oss-cn-hangzhou.aliyuncs.com/testfile/e04cc608-5842-48fb-929d-276d94ec1918.docx</div>
    <div
      @click="clickUrl('https://ymr-test.oss-cn-hangzhou.aliyuncs.com/testfile/592af889-c6fa-42e5-81ea-849bc9524551.txt')"
    >https://ymr-test.oss-cn-hangzhou.aliyuncs.com/testfile/592af889-c6fa-42e5-81ea-849bc9524551.txt</div>
    <Preview :url="url" @hidePreview="hidePreview"></Preview>
  </div>
</template>

<script>
import Preview from "@/components/Preview";

export default {
  name: "App",
  components: {
    Preview,
  },
  data() {
    return {
      imgUrl:
        "https://ymr-test.oss-cn-hangzhou.aliyuncs.com/test-image/de5df880-2dbb-4607-9e1d-9bd77233d20d.jpg",
      url: "",
    };
  },
  methods: {
    clickUrl(url) {
      this.url = url;
    },

    hidePreview() {
      this.url = "";
    },
  },
};
</script>

<style lang="scss">
</style>
