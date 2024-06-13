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
