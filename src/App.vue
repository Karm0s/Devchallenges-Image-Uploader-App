<template>
  <div id="app" class="antialiased h-screen w-screen flex items-center justify-center bg-gray-200">
    <UploadForm/>
  </div>
</template>

<script>
import UploadForm from './components/UploadForm';

export default {
  name: 'App',
  components: {
    UploadForm
  }
}
</script>

<style>
#app{
  font-family: 'Poppins', sans-serif;
}
</style>
