<script setup>
import { reactive } from 'vue';
import InputNew from './InputNew.vue';


let columns = reactive([
    {
        id: crypto.randomUUID(),
        title: 'Column #1',
        items: [
            {
                id: crypto.randomUUID(),
                title: "Feature"
            },
            {
                id: crypto.randomUUID(),
                title: "Solve bug !!"
            }
        ] 
    },
    {
        id: crypto.randomUUID(),
        title: 'Column #2',
        items: [
            {
                id: crypto.randomUUID(),
                title: "Send report"
            },
            {
                id: crypto.randomUUID(),
                title: "Code review"
            }
        ] 
    }
])

function handleNewItem(text, column){
    column.items.push({
        id: crypto.randomUUID(),
        title: text.value
    })
}

function handleNewColumn(){
    const title = prompt('Name:')
    if(!!title){
        columns.push({
            id: crypto.randomUUID(),
            title: title,
            items: []
        })
    }
}

function startDrag(evt, column, item){
    evt.dataTransfer.setData("text/plain", JSON.stringify({
        columnId: column.id,
        itemId: item.id
    }))
}

function onDrop(evt, dest){
    const {columnId, itemId} = JSON.parse(evt.dataTransfer.getData('text/plain'))
    //console.log(columnId, itemId);
    const originColumn = columns.find(item => item.id == columnId)
    const originItem = originColumn.items.find(item => item.id == itemId)

    console.log(originColumn);
    console.log(originColumn.title, originItem.title);

    dest.items.push({...originItem})
    originColumn.items = originColumn.items.filter((item) => item != originItem)
}

</script>

<template>
    <nav>
        <ul>
            <li>
                <a href="" @click.prevent="handleNewColumn">Create Board</a>
            </li>
        </ul>
    </nav>

    <div class="column-container">
        <div class="columns">
            <div 
                class="column" 
                @drop="onDrop($event, column)" 
                @dragover.prevent 
                @dragenter.prevent 
                v-for="column in columns" 
                :key="column.id">

                <div class="">{{column.title}}</div>
                <InputNew @on-new-item="(text) => handleNewItem(text, column)" />
                <div class="items">
                    <div class="item" draggable="true" @dragstart="startDrag($event, column, item)" v-for="item in column.items" :key="item.id">
                        {{item.title}}
                    </div>
                </div>
                
            </div>
        </div>
    </div>
</template>

<style scoped>
    .columns {
        display: flex;
        gap: 10px;
    }

    .column{
        background-color: #efefef;
        padding: 10px;
    }

    .items {
        display: flex;
        flex-direction: column;
        gap: 5px;
    }

    .item {
        background-color: white;
        padding: 10px;
        box-sizing: border-box;
    }
</style>