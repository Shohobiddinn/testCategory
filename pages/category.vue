<template>
    <div class="flex">
        <div class="p-4 max-w-md mx-auto bg-white rounded-xl shadow-md space-y-4" v-if="false">

            <pre>{{ categories }}</pre>
        </div>
        <div class="p-4 max-w-md mx-auto bg-white rounded-xl shadow-md space-y-4">
            <div>
                <button @click="categoryAll" v-if="statusAll" class="h-[40px]"><i class="fa-solid fa-reply-all"></i>
                    Barchasi </button>
                <div v-for="parentCategory in parentCategories">
                    <button @click="categoryParent(parentCategory)" class="h-[40px] "><i
                            class="fa-solid fa-chevron-left"></i> {{ parentCategory.name }}
                    </button>

                </div>
            </div>
            <CategoryItem v-for="category in categories" :key="category.id" :category="category"
                @update="handleUpdateMessage" />
        </div>

    </div>
</template>

<script>
import CategoryItem from '~/components/CategoryItem.vue';
import categoryData from '~/static/categories.json';
export default {
    name: 'IndexPage',
    components: {
        CategoryItem
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
            //    let Cat = this.categories.find(item => item.id == message.id);
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
                this.parentCategories.length =  index + 1;
            }
        }
    }
};
</script>