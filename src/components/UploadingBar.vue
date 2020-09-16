<template>
  <div
    class="card shadow-xl rounded-lg flex flex-col justify-start bg-white px-10 py-6"
  >
    <h1 class="mb-6">Uploading...</h1>

    <div class="progress-bar mb-6"></div>
  </div>
</template>

<script>
export default {
  name: 'UploadingBar'
}
</script>

<style scoped>
.progress-bar.progress-bar:before{
  z-index: 1;
  height: 5px;
  width: 90%;
  margin: 0;
  border-radius: 500px;
}
.progress-bar{
  z-index: 1;
  border-radius: 500px;
  background-color: #F2F2F2;
  display: flex;
  overflow: hidden;

}
.progress-bar:before{
  background-color: #2F80ED;
  content: '';
  -webkit-animation: running-progress 2s cubic-bezier(0.4, 0, 0.2, 1) infinite;
  animation: running-progress 2s cubic-bezier(0.4, 0, 0.2, 1) infinite;
}
@-webkit-keyframes running-progress {
  0% { margin-left: 0px; margin-right: 100%; }
  50% { margin-left: 25%; margin-right: 0%; }
  100% { margin-left: 100%; margin-right: 0; }
}
@keyframes running-progress {
  0% { margin-left: 0px; margin-right: 100%; }
  50% { margin-left: 25%; margin-right: 0%; }
  100% { margin-left: 100%; margin-right: 0; }
}
</style>