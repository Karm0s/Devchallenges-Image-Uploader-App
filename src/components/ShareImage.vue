<template>
  <div
    class="card shadow-xl rounded-lg flex flex-col items-center justify-start bg-white px-10"
  >

    <h1 class="text-lg mt-5">Uploaded Successfully!</h1>
    <img src="../assets/tick.svg" class="check-icon px-2 mt-5" alt="">

    <img :src="imageLink" class="rounded-lg mt-5" alt="">

    <div class="flex items-center justify-between w-full rounded-lg border-2 mt-5 mb-5">
      <div class="link px-5">
        <p>{{imageLink}}</p>
      </div>
      <button class="btn text-xs text-white bg-blue-500 rounded-lg mx-1 my-1 cursor-pointer" @click="copyLink">Copy Link</button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'ShareImage',
  props: ['imageLink'],
  methods: {
    copyLink(){
    }
  }
};
</script>

<style scoped>
.check-icon{
  background-color: #219653;
  width: 40px;
  height: 40px;
  border-radius: 100%;
}
.link{
  text-overflow: ellipsis;
  overflow: hidden; 
  max-width: 70%;
  height: 1.2em; 
  white-space: nowrap;
  font-size: 10px;
}
</style>
