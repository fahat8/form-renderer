<template>
    <div class="container">
        <!-- Droppable Section 1 -->
        <div class="drop-zone" @drop="onDrop($event, 1)" @dragover.prevent="() => { }" @dragenter.prevent="() => { }">
            <div v-for="item in getList(1)" :key="item.id" class="drag-el" draggable="true"
                @dragstart="startDrag($event, item)">
                {{ item.title }}
            </div>
        </div>
        <!-- Droppable Section 2 -->
        <div class="drop-zone" @drop="onDrop($event, 2)" @dragover.prevent="() => { }" @dragenter.prevent="() => { }">
            <div v-for="item in getList(2)" :key="item.id" class="drag-el" draggable="true"
                @dragstart="startDrag($event, item)">
                {{ item.title }}
            </div>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue'

export default {
    setup() {
        const items = ref([
            { id: 0, title: 'Item A', list: 1 },
            { id: 1, title: 'Item B', list: 1 },
            { id: 2, title: 'Item C', list: 2 },
        ])

        const getList = (list) => {
            return items.value.filter((item) => item.list == list)
        }

        const startDrag = (evt, item) => {
            evt.dataTransfer.dropEffect = 'move'
            evt.dataTransfer.effectAllowed = 'move'
            evt.dataTransfer.setData('itemID', item.id.toString())
        }

        const onDrop = (evt, list) => {
            const itemID = parseInt(evt.dataTransfer.getData('itemID'))
            const item = items.value.findIndex((item) => item.id === itemID)
            if (item !== -1) {
                // Ensure we're modifying the object, not overwriting an array index
                items.value[item].list = list;
                console.log('Updated item:', items.value[item]);
            } else {
                console.log('Item not found with ID:', itemID);
            }
        }

        return {
            getList,
            onDrop,
            startDrag,
        }
    },
}
</script>

<style>
.drop-zone {
    width: 50%;
    margin: 50px auto;
    background-color: #eee;
    margin-bottom: 10px;
    padding: 10px;
    min-height: 10px;
}

.drag-el {
    background-color: #fff;
    margin-bottom: 10px;
    padding: 5px;
}
</style>
