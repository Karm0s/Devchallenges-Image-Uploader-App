<template>
  <div
    class="card shadow-xl rounded-lg flex flex-col items-center justify-start bg-white px-10"
  >
    <h1 class="text-lg mt-5">Upload your image</h1>
    <div
      class="error rounded-md bg-red-500 text-white text-center text-sm w-full mt-5"
      v-if="error"
    >
      <div class="mx-5 my-5">
        Sorry but the uploaded file is not supported.
      </div>
    </div>

    <h3 class="text-xs text-gray-700 mt-5">File should be Jpeg, Png...</h3>

    <div
      class=" w-full bg-gray-200 rounded-lg mt-5 border-2 border-dashed px-10"
      :class="{
        'border-blue-500': fileOverDropArea,
        'border-gray-500': !fileOverDropArea,
      }"
      @drop.prevent="dropFile"
      @dragover.prevent
      @dragenter.prevent="fileOverDropArea = true"
      @dragleave.prevent="fileOverDropArea = false"
    >
      <div
        class="flex flex-col flex-grow items-center justify-center dropzone-child-elements py-10"
      >
        <img src="../assets/image.svg" alt="" />
        <div class="mt-10 text-gray-500">
          Drag & Drop your image here
        </div>
      </div>
    </div>

    <h3 class="text-xs text-gray-700 my-5">Or</h3>

    <input
      id="fileUpload"
      type="file"
      ref="file"
      hidden
      @change="handleFileUpload"
    />

    <button
      class="btn text-xs text-white bg-blue-500 rounded-lg mb-5 cursor-pointer"
      @click="chooseFile"
    >
      <p>Choose a file</p>
    </button>
  </div>
</template>

<script>
// import axios from "axios";

export default {
  name: "UploadForm",
  data() {
    return {
      file: null,
      fileOverDropArea: false,
      error: false,
    };
  },

  methods: {
    chooseFile() {
      document.getElementById("fileUpload").click();
    },
    dropFile(e) {
      let droppedFiles = e.dataTransfer.files;
      if (!droppedFiles) return;
      this.file = droppedFiles[0];
      this.uploadFile();
    },
    handleFileUpload() {
      this.file = this.$refs.file.files[0];
      this.uploadFile();
    },
    uploadFile() {
      this.error = false;
      if (this.file.type !== "image/png" && this.file.type !== "image/jpeg") {
        this.error = true;
        return;
      }

      this.$emit('onFileUpload', this.file);
    },
  },
};
</script>

<style>
.card {
  width: 402px;
}
.btn {
  width: 100px;
  height: 31px;
}
.dropzone-child-elements {
  pointer-events: none;
}
</style>
