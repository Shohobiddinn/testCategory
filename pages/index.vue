<template>
    <div class="p-10">

        <RouterLink class="bg-blue-700 text-white px-4 py-2 rounded-lg hover:underline " to="/category">
            Kategoriyalar <i class="fa-solid fa-layer-group text-[13px] ml-1"></i>
        </RouterLink>
        <div class="p-4 max-w-md  bg-gray-100 mt-3 rounded-xl shadow-md space-y-4">
            <div>
                <button @click="categoryAll" v-if="statusAll"
                    class="h-[40px] cursor-pointer group  bg-blue-400 px-3 rounded-md py-2 text-white w-[50%] text-start text-[18px]">
                        <i class="fa-solid fa-bars text-[15px] group-hover:text-[18px] duration-100"></i>
                    Barchasi </button>
                <div class="mt-1 group" v-for="(parentCategory, index) in parentCategories" :class="{
                    'cursor-pointer bg-blue-300 px-3 rounded-md py-1 text-white ': (index + 1) == parentCategories?.length
                }">
                    <button @click="categoryParent(parentCategory)" class="h-[40px] "><i
                            class="fa-solid fa-chevron-left group-hover:translate-x-[-3px] duration-100"></i> {{ parentCategory.name }}
                    </button>

                </div>
            </div>
            <PageItem v-for="category in categories" :key="category.id" :category="category"
                @update="handleUpdateMessage" />
        </div>
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
            categories: categoryData.categories,
            statusAll: false,
            parentCategories: []
        };
    },
    methods: {
        handleUpdateMessage(message) {
            this.parentCategories.push(message)
            this.categories = message.children;
            this.statusAll = true;
        },
        categoryAll() {
            this.categories = categoryData.categories;
            this.parentCategories = []
            this.statusAll = false;
        },
        categoryParent(item) {
            this.categories = item.children;
            let index = this.parentCategories.findIndex(parent => parent.id == item.id)
            if (index > -1) {
                this.parentCategories.length = index + 1;
            }
        }
    }
};
</script>
