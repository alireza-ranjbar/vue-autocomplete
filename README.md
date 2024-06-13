# AutoCompleteComponent

AutoCompleteComponent is a Vue 3 component for creating an autocomplete input field. It allows users to filter and select items from a list as they type in the input field.

## Installation

To use the AutoCompleteComponent, you need to create a Vue 3 project.

## Usage
### Component File
Add the following code as AutoCompleteComponent.vue:
```javascript
<script setup>
import { ref } from 'vue';
const emit = defineEmits(['fetchItemsFunction'])

const inputValue = ref('')
const showList = ref(false)

const fetchList = () => {
    emit('fetchItemsFunction', inputValue)
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
    items: Array,
})
</script>

<template>
    <label for="autocomplete-input" class="form-label">
        <span class="text-muted text-small">{{ label }}</span>
    </label>
    <input id="autocomplete-input" v-model="inputValue" @input="fetchList" @focus="showList = true" @blur="handleBlur"
    type="text" class="form-control position-relative" autocomplete="off">
    <ul v-if="showList" class="show-list rounded-2 border position-absolute">
        <li v-for="item in items" :key="item.id" @click="selectItem(item)">{{ item.name }}</li>
    </ul>
</template>

<style scoped>
#autocomplete-input {
    border: 1px solid v-bind(color);
    height: 45px;
    width: 100%;
}

.show-list {
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

.show-list li {
    padding: 5px 10px;
    cursor: pointer;
}

.show-list li:hover {
    background-color: #E9E5FC;
}
</style>
```

# App File
Import the AutoCompleteComponent in each parent component like App.vue and update the parent component file as follows:

```javascript
<script setup>
import AutoCompleteComponent from '@/components/AutoCompleteComponent.vue'
import { ref } from 'vue';

const contacts = ref([])
const contactName = ref('')
const fetchedContacts = ref([])

const fetchContacts = async(inputValue) => {
    contacts.value = [
      {id:1 ,name:'John'},
      {id:2 ,name:'Sarah'},
      {id:3 ,name:'Mike'},
      {id:4 ,name:'Lindsey'},
      {id:5 ,name:'Frank'},
      {id:6 ,name:'Joe'},
    ]

    //use inputValue to create a query on fetchedContacts array and retrun matched items
    fetchedContacts.value = contacts.value.filter(item => 
      item.name.toLowerCase().includes(inputValue.value.toLowerCase())
    );
}
</script>

<template>
  <div id="app" class="container">
    <div class="row">
      <div class="mt-3 position-relative px-0">
        <AutoCompleteComponent label="Contacts name" color="#E9E5FC" :items="fetchedContacts" @fetchItemsFunction="fetchContacts"/>
      </div>
    </div>

  </div>

</template>

```

## Props
* label: The label for the input field
* color: The border color of the input field
* items: The list of items for autocomplete

## Events
* fetchItemsFunction:Emits the input value to fetch the matching items


[MIT](https://choosealicense.com/licenses/mit/)