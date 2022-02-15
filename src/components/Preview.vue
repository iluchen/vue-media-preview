<template>
  <div v-show="showMask" class="preview-wrap">
    <div class="mask">
      <img ref="img" v-if="type === 'img'" :src="url" alt="暂无图片" />
      <video v-else-if="type === 'video'" controls :src="url"></video>

      <iframe class="frame" ref="iframe" src="" frameborder="0"></iframe>
    </div>
    <span class="close-btn preview-iconfont icon-shanchu" @click="hidePreview"></span>
    <!-- <div class="close-btn" @click="hidePreview">关闭</div> -->
  </div>
</template>

<script>
import "../assets/font/iconfont.css";

export default {
  name: "vue-media-preview",

  props: {
    url: {
      type: String,
      default: ""
    },

    // 是否可调整大小
    resize: {
      type: Boolean,
      default: false
    }
  },

  data() {
    return {
      showMask: false,
      type: "", // img video
      imgSuffix: ["gif", "jpg", "jpeg", "png", "webp"],
      videoSuffix: ["mp4", "webm"],
      docSuffix: ["docx", "dotx", "xlsx", "xls", "pptx", "ppsx", "ppt", "pps"],
      officeBaseUrl: "https://view.officeapps.live.com/op/view.aspx?src="
    };
  },

  watch: {
    url(v) {
      this.validMediaType(v);
    }
  },

  methods: {
    hidePreview() {
      this.showMask = false;
      // 移除 url
      this.$emit("hidePreview");
    },
    // 校验文件类型， img video  展示，doc 跳转office 链接，其余默认跳转
    validMediaType(v) {
      if (!v) {
        return;
      }

      if(/^data:image/.test(v)) {
        this.type = "img";
        this.showMask = true;
        return
      }

      const reg = /\.[^\.]+$/;
      const suffix = reg
        .exec(v)[0]
        .substring(1)
        .toLowerCase();
      if (this.imgSuffix.includes(suffix)) {
        this.type = "img";
        this.showMask = true;
      } else if (this.videoSuffix.includes(suffix)) {
        this.type = "video";
        this.showMask = true;
      } else if (this.docSuffix.includes(suffix)) {
        window.open(this.officeBaseUrl + this.url, "_blank");
      } else {
        window.open(this.url, "_blank");
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.preview-wrap {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6);
  z-index: 9999;
  .mask {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;

    img {
      max-width: 80%;
      max-height: 80%;
      position: relative;
      z-index: 66;
    }

    video {
      max-width: 80%;
      max-height: 80%;
      position: relative;
      z-index: 66;
    }

    .frame {
      position: absolute;
      width: 100%;
      height: 100%;
      left: 0;
      top: 0;
      z-index: 6;
    }
  }
  .close-btn {
    position: absolute;
    right: 60px;
    top: 60px;
    font-size: 36px;
    transition: all 0.5s;
    color: #ffffff;
    z-index: 66;

    &:hover {
      color: red;
      cursor: pointer;
      transform: rotate(90deg);
    }
  }
}
</style>
