<template>
  <div
    id="app"
    class="antialiased h-screen w-screen flex flex-col items-center justify-center bg-gray-200"
    @dragover.prevent
    @drop.prevent
  >
    <div
      class="error rounded-md bg-red-500 text-white text-center text-sm mb-5"
      v-if="error"
    >
      <div class="mx-5 my-5">
        Server Error: Sorry but the uploaded file is not supported.
      </div>
    </div>

    <UploadForm v-if="uploadStatus === 'waiting'" @onFileUpload="handleFileUpload" />

    <UploadingBar v-if="uploadStatus === 'uploading'"/>

    <ShareImage v-if="uploadStatus === 'done'" :imageLink="imageLink"/>
  </div>
</template>

<script>
import axios from "axios";
import UploadForm from "./components/UploadForm";
import UploadingBar from "./components/UploadingBar";
import ShareImage from "./components/ShareImage";

export default {
  name: "App",
  data() {
    return {
      uploadStatus: "waiting",
      imageLink: '',
      error: false,
    };
  },
  components: {
    UploadForm,
    UploadingBar,
    ShareImage
  },
  methods: {
    handleFileUpload(file) {
      this.error = false;
      this.uploadStatus = "uploading";
      let form = new FormData();
      form.append("image", file, this.fileName);
      axios
        .post(`${process.env.VUE_APP_BACKEND_API}/api/images`, form)
        .then(({ data }) => {
          this.imageLink = data.link;
          this.uploadStatus = 'done';
        })
        .catch(() => {
          this.error = true;
          this.uploadStatus = 'waiting';
        });
    },
  },
};
</script>

<style>
#app {
  font-family: "Poppins", sans-serif;
}
</style>
