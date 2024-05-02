<template>
    <div>
        <button @click="addPage">Add Page</button>
        <page-editor v-for="(page, index) in pages" :key="index" :page="page" @updatePage="updatePage(index, $event)" />
        <button @click="generateJson">Generate JSON</button>
        <pre>{{ JSON.stringify(jsonOutput, null, 2) }}</pre>
    </div>
</template>

<script>
import PageEditor from './SurveyJsonGeneratorComponents/PageEditor.vue';

export default {
    components: {
        PageEditor
    },
    data() {
        return {
            pages: [],
            jsonOutput: {}
        };
    },
    methods: {
        addPage() {
            this.pages.push({ name: `page${this.pages.length + 1}`, elements: [] });
        },
        updatePage(index, page) {
            this.pages.splice(index, 1, page);
        },
        generateJson() {
            this.jsonOutput = {
                pages: this.pages,
                showQuestionNumbers: "off"
            };
        }
    }
};
</script>