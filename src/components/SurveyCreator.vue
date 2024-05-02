<template>
    <div class="container" style="display: flex;">
        <!-- Source Column (Left) -->
        <div class="drop-zone" style="width: 50%; float: left;">
            <div v-for="item in getList(1)" :key="item.id" class="drag-el" draggable="true"
                @dragstart="startDrag($event, item, 1)">
                {{ item.title }}
            </div>
        </div>
        <!-- Target Column (Right) -->
        <div class="drop-zone" @drop="onDrop($event)" @dragover.prevent="() => { }" @dragenter.prevent="() => { }"
            style="width: 50%; float: right;">
            <div v-for="item in getList(2)" :key="`target-${item.id}`" class="drag-el" draggable="true"
                @dragstart="startDrag($event, item, 2)" @dragover="dragOver($event, index)">
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
            { id: 3, title: 'Item C', list: 1 },
            { id: 4, title: 'Item D', list: 1 },
            { id: 5, title: 'Item E', list: 1 }
        ]);

        const nextId = ref(6);
        const dropIndex = ref(-1);

        const getList = (list) => {
            return items.value.filter(item => item.list === list);
        }

        const startDrag = (evt, item, origin) => {
            evt.dataTransfer.dropEffect = 'move';
            evt.dataTransfer.effectAllowed = 'all';
            evt.dataTransfer.setData('itemID', item.id.toString());
            evt.dataTransfer.setData('origin', origin.toString());
        }

        const dragOver = (evt, index) => {
            dropIndex.value = index; // TODO: Fix - value is always undefined, not the value of the element on which it is hovered. Currently, the element is dragged on top of the list
            evt.preventDefault();
            console.log(dropIndex.value);
        }

        const onDrop = (evt) => {
            const itemID = parseInt(evt.dataTransfer.getData('itemID'));
            const origin = parseInt(evt.dataTransfer.getData('origin'));
            const droppedItem = items.value.find(item => item.id === itemID);

            if (droppedItem) {
                if (origin === 1 && droppedItem.list === 1) { // From left to right
                    const newItem = { ...droppedItem, id: nextId.value++, list: 2 };
                    items.value.push(newItem);
                } else if (origin === 2) { // Reorder elements in right list
                    items.value.splice(items.value.findIndex(i => i.id === itemID), 1);
                    items.value.splice(dropIndex.value, 0, droppedItem);
                }
            }
        }

        return {
            getList,
            onDrop,
            startDrag,
            dragOver,
        }
    },
}
</script>



<style>
.container {
    display: flex;
    justify-content: space-between;
}

.drop-zone {
    width: 50%;
    margin: 0;
    background-color: #eee;
    padding: 10px;
    min-height: 100px;
    /* Ensure there's space to drop */
}

.drag-el {
    background-color: #fff;
    margin-bottom: 10px;
    padding: 5px;
    cursor: pointer;
    /* Indicates it's draggable */
}
</style>
