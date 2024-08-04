<template>
  <div class="p-4 max-w-md mx-auto bg-white rounded-xl shadow-md space-y-4">
    <PageItem v-for="category in categories" :key="category.id" :category="category" />
  </div>
</template>

<script>
import PageItem from '~/components/PageItem.vue';
import categoryData from '~/static/categories.json';

export default {
  name: 'IndexPage',
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
