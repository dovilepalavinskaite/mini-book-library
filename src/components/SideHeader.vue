<template>
  <div class="sideheader-container d-flex flex-column align-items-centers pt-3">
   <img src="../assets/random-logo.png" alt="Random logo">
   <div class="menu-itmes text-center mt-4">
    <div class="py-2" @click="setActivePage('homepage')"><i class="fa-solid fa-house"></i></div>
    <div class="py-2" @click="setActivePage('books-list')"><i class="fa-solid fa-book"></i></div>
    <div class="py-2" @click="setActivePage('books-form')"><i class="fa-solid fa-pen"></i></div>
   </div>
  </div>
</template>

<script>
export default {
  name: 'SideHeader',
  methods: {
    setActivePage(page) {
      this.$emit('set-page', page);
    }
  }
}
</script>

<style scoped>

.sideheader-container {
  background-color: #f2f0eb;
  width: 70px;
}

i {
  color: #dedede;
  cursor: pointer;
}

i:hover {
  color: #d3d3d3;
}

</style>
