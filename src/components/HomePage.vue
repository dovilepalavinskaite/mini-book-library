<template>
  <div class="pl-4 pt-4">
    <h4>Your personal Books Database</h4>
    <hr class="divider">
    <div>
      <img src="../assets/banner.jpg" alt="Banner">
    </div>
    <div class="text-center">
      <div class="d-flex pt-5">
        <div v-for="process in processList" :key="process.id" class="process-container p-4 d-flex flex-column text-center mr-5 text-light">
          <span>{{ process.id }}.</span>
          <p>{{ process.step }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
  
<script>

  export default {
    name: 'HomePage',
    data() {
      return {
        processList: [
          {
            id: 1,
            step: 'Register your book'
          },
          {
            id: 2,
            step: 'See your full book list'
          },
          {
            id: 3,
            step: 'Filter books by categories'
          },
          {
            id: 4,
            step: 'Enjoy reading!'
          }
        ]
      }
    }
}
</script>
  
<style scoped>

.divider {
  width: 33%;
}
.process-container {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  background: #7c9d96;
}

img {
  width: 690px;
}

</style>
  