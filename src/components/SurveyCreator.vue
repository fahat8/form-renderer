<template>
    <div class="drop-zone" @drop="onDrop($event, 1)" @dragover.prevent @dragenter.prevent>
        <div class="drop-zone">
            <div v-for="item in getList(1)" :key="item.id" class="drag-el" draggable="true"
                @dragstart="startDrag($event, item)">
                {{ item.title }}
            </div>
        </div>
    </div>
    <div class="drop-zone" @drop="onDrop($event, 2)" @dragover.prevent @dragenter.prevent>
        <div class="drop-zone">
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
        const items: ref([
            {
                id: 0,
                title: 'Item A',
                list: 1,
            },
            {
                id: 1,
                title: 'Item B',
                list: 1,
            },
            {
                id: 2,
                title: 'Item C',
                list: 2,
            },
        ])

        const getList = (list) => {
            return ItemsField.value.filter((item) => item.list == list)
        }

        const startDrag = (evt, item) => {
            console.log(item)
            evt.dataTransfer.dropEffect = 'move'
            evt.dataTransfer.effectAllowed = 'move'
            evt.dataTransfer.setData('itemID', item.id)
        }

        const onDrop = (evt, list) => {
            console.log(item)
            const itemID = evt.dataTransfer.getData('itemID')
            const item = this.items.find((item) => item.id == itemID)
            item.list = list
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
    margin: 50 px auto;
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
