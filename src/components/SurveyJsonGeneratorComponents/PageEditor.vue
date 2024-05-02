<template>
    <div>
        <input v-model="localPage.name" placeholder="Enter page name">
        <button @click="addElement">Add Element</button>
        <element-editor v-for="(element, index) in localPage.elements" :key="index" :element="element"
            @updateElement="updateElement(index, $event)" />
    </div>
</template>

<script>
import ElementEditor from './ElementEditor.vue';

export default {
    props: ['page'],
    components: {
        ElementEditor
    },
    data() {
        return {
            localPage: JSON.parse(JSON.stringify(this.page))
        };
    },
    methods: {
        addElement() {
            this.localPage.elements.push({ type: "text", name: "", choices: [] });
        },
        updateElement(index, element) {
            this.localPage.elements.splice(index, 1, element);
            this.$emit('updatePage', this.localPage);
        }
    },
    watch: {
        page: {
            handler(newVal) {
                this.localPage = JSON.parse(JSON.stringify(newVal));
            },
            deep: true
        }
    }
};
</script>