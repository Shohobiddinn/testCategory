<template>
  <div>
    <div @click="toggle(propsCategory)"
      class="cursor-pointer hover:bg-blue-300 px-3 rounded-md py-2 flex items-center justify-between group">
      <span class="">{{ propsCategory.name }}</span>
      <span v-if="propsCategory?.children?.length"
        class="transform transition-transform group-hover:translate-x-[3px] duration-100"
        :class="{ 'rotate-90': isOpen }">
        <i class="fa-solid fa-chevron-right  hover "></i>
      </span>
    </div>
  </div>
</template>

<script lang="ts">
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
    toggle(item: any) {
      this.isOpen = !this.isOpen;
      if (item.children.length) {
        this.$emit('update', item);
      }
    }
  },
};
</script>

<style scoped></style>