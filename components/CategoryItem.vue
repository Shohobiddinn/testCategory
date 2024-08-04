<template>
  <div>
    <div @click="toggle" class="cursor-pointer py-2 flex items-center justify-between">
      <span>{{ category.name }}</span>
      <span v-if="category.children.length" class="transform transition-transform" :class="{ 'rotate-90': isOpen }">
        <i class="fa-solid fa-chevron-right"></i>
      </span>
    </div>
    <div v-if="isOpen" class="ml-4 border-l-2 pl-4">
      <CategoryItem v-for="child in category.children" :key="child.id" :category="child" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'CategoryItem',
  props: {
    category: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      isOpen: false
    };
  },
  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
    }
  },
  components: {
    CategoryItem: () => import('./CategoryItem.vue')
  }
};
</script>

<style scoped>
.cursor-pointer:hover {
  background-color: #f0f0f0;
}
</style>