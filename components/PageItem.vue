
<template>
    <div>
      <div @click="toggle(propsCategory)" class="cursor-pointer hover:bg-blue-300 px-3 rounded-md py-2 flex items-center justify-between group">
        <span class="">{{ propsCategory.name }}</span>
        <span v-if="propsCategory?.children?.length" class="transform transition-transform group-hover:translate-x-[3px] duration-100"
          :class="{ 'rotate-90': isOpen }">
          <i class="fa-solid fa-chevron-right  hover " ></i>
        </span>
      </div>
      <div v-if="isOpen" class="ml-4 border-l-2 pl-4">
        <PageItem v-for="child in propsCategory?.children" :key="child.id" :category="child" />
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'PageItem',
    props: {
      category: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        isOpen: false,
        propsCategory: this.category
      };
    },
    methods: {
      toggle(item) {
        this.isOpen = !this.isOpen;
        if (item.children.length) {
          this.$emit('update', item);
  
        }
        // let Cat = this.props.category.children.find(cat => cat.id == item.id)
        // this.props.category = [Cat]
        // this.propsCategory = [item.children]
  
      }
    },
    components: {
      CategoryItem: () => import('./CategoryItem.vue')
    }
  };
  </script>
  
  <style scoped>
  </style>