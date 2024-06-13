<script setup>
import { ref } from 'vue';
const emit = defineEmits(['fetchItemsFunction'])

const inputValue = ref('')
const showList = ref(false)

const fetchList = () => {
    emit('fetchItemsFunction',inputValue)
}
const handleBlur = () => {
    setTimeout(() => {
        showList.value = false;
    }, 100);
}
const selectItem = (item) => {
    inputValue.value = item.name
}

const props = defineProps({
    label: String,
    color: String,
    inputValue: String,
    items: Array,
})
</script>

<template>
    <!-- parent padding x must be 0 -->
     <!-- access input value for fetching new query -->
    <label for="autocomplete-input" class="form-label">
        <span class="text-muted text-small">{{ label }}</span>
    </label>
    <input id="autocomplete-input" v-model="inputValue" @input="fetchList" @focus="showList = !showList" @blur="handleBlur"
    type="text" class="form-control position-relative" autocomplete="nope">
    <ul v-if="showList" class="show-list rounded-2 border position-absolute">
        <li v-for="item in items" :key="item.id" @click="selectItem(item)">{{ item.name }}</li>
    </ul>
</template>

<style scoped>
#autocomplete-input{
    border: 1px solid v-bind(color);
    height: 45px;
    width: 100%;
}
.show-list{
    list-style: none;
    text-align: left;
    padding: 0;
    max-height: 150px;
    background-color: white;
    overflow: auto;
    top: 82px;
    left: 0;
    width: 100%;
}
.show-list li{
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 5px;
    padding-bottom: 5px;
    cursor: pointer;
}
.show-list li:hover{
    background-color: #E9E5FC;
}
</style>
