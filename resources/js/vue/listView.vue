<template>
  <div>
      <div>
        <div v-for="(item, index) in items" :key="index">
          <ListItem 
            :item="item"
            class=""
            v-on:itemchanged="$emit('reloadList')"
          />
        </div>
      </div>
  </div>
</template>

<script>
// import listItem from './listItem'
import ListItem from './listItem.vue'
export default {
  props: ['items'],
  components: {
    ListItem,
  }
}
</script>

<style>

</style>