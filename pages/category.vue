
<template>
  <div class="p-10">
    <RouterLink class="bg-blue-700  text-white px-4 py-2 rounded-lg hover:underline " to="/">
             Bosh sahifa <i class="fa-solid fa-house text-[13px] ml-1"></i>
         </RouterLink>
     <div class="p-4 max-w-md  bg-white rounded-xl shadow-md space-y-4">
       <PageItem v-for="category in categories" :key="category.id" :category="category" />
     </div>

  </div>
  </template>
  
  <script>
  import PageItem from '~/components/PageItem.vue';
  import categoryData from '~/static/categories.json';
  
  export default {
    name: 'CategoryPage',
    components: {
      PageItem
    },
    data() {
      return {
        categories: categoryData.categories
      };
    }
  };
  </script>
  