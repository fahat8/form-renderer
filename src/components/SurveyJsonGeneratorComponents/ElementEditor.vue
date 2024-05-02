<template>
    <div>
        <select v-model="localElement.type">
            <option value="checkbox">Checkbox</option>
            <option value="text">Text</option>
            <option value="dropdown">Dropdown</option>
            <option value="panel">Panel</option>
        </select>
        <input v-model="localElement.name" placeholder="Enter element name">
        <!-- Additional controls based on type can be added here -->
        <button @click="$emit('updateElement', localElement)">Save Element</button>
    </div>
</template>

<script>
export default {
    props: ['element'],
    data() {
        return {
            localElement: JSON.parse(JSON.stringify(this.element))
        };
    },
    watch: {
        element: {
            handler(newVal) {
                this.localElement = JSON.parse(JSON.stringify(newVal));
            },
            deep: true
        }
    }
};
</script>