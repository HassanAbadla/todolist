<template>
  <div id="todoListContainer" class="w-3/5 h-screen bg-yellow-400 border-1 rounded-lg m-auto p-12">
    <div id="heading" class="bg-gray-50 flex flex-col justify-between p-6 rounded-xl">
      <h2 id="title" class="text-center font-bold text-2xl">Todo List</h2>
      <addItemForm v-on:reloadList="getList()" />
    </div>
    <list-View 
      :items="items"
      v-on:reloadList="getList()"
     />
  </div>
</template>

<script>
import addItemForm from './addItemForm'
import listView from './listView'

export default {
  components: {
    addItemForm,
    listView
  },
  data() {
    return {
      items: []
    }
  },
  methods: {
    getList() {
      axios.get('api/items').then( response => {
        this.items = response.data
      })
      .catch( error => { console.log(error) })
    }
  },
  created() {
    this.getList();
  }

}
</script>

<style>

</style>