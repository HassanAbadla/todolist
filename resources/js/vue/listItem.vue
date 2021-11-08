<template>
  <div class="w-full bg-gray-50 p-4 my-2 rounded-xl">
      <div>
        <input type="checkbox" @change="updateCheck()" v-model="item.completed" class="mx-2" />
        
        <span :class="[ item.completed ? 'completed' : '', 'itemText']" > {{ item.name }} </span>
        <button @click="removeItem()" class="float-right">
          <font-awesome-icon icon="trash" color="red" />
        </button>
      </div>
  </div>
</template>

<script>
export default {
  props: ['item'],
  methods: {
    updateCheck() {
      axios.put('api/item/' + this.item.id, {
        item: this.item
      })
      .then( response => {
        if( response.status == 200 ) {
          this.$emit('itemchanged');
        }
      })
      .catch(error => {
        console.log(error);
      })
    },
    removeItem() {
      axios.delete('api/item/' + this.item.id)
      .then(response => {
        if(response.status == 200) {
          this.$emit('itemchanged');
        }
      })
      .catch (error => {
        console.log(error);
      })
    }
  }
}
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: #999999;
}

</style>