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

</script>

<template>
    <nav>
        <ul>
            <li>
                <a href="">Create Board</a>
            </li>
        </ul>
    </nav>

    <div class="column-container">
        <div class="columns">
            <div class="column" v-for="column in columns" :key="column.id">
                <div class="">{{column.title}}</div>
                <InputNew />
                <div class="items">
                    <div class="item" v-for="item in column.items" :key="item.id">
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