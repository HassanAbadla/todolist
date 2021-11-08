<template>
  <div id="addItem" class="flex justify-evenly pt-6">
    <div class="m-auto">
      <input type="text" placeholder="Placeholder" v-model="item.name"
      class="w-96 px-4 mr-6 py-1 rounded-lg border border-yellow-300 focus:outline-none focus:ring-2 focus:ring-yellow-200" />
      
        <font-awesome-icon 
        @click="addItem()"
        icon = "plus-square" 
        size="lg" 
        :class="[ item.name ? 'active': 'inactive', 'plus' ]"
        />
      </div>
  </div>
</template>

<script>
export default {
  data()  {
    return {
      item: {
        name: ""
      }
    }
  },
  methods: {
    addItem() {
      if(this.item.name =='') {
        return;
      }

      axios.post('api/item/store', {
        item: this.item
      })
      .then(response => {
        if(response.status ==201) {
          this.item.name ='';
          this.$emit('reloadList');
        }
      })
      .catch( error => {
        console.log(error);
      })
    }
  }
}
</script>

<style scoped>
.active{
  color:rgb(11, 167, 81)
}
.inactive {
  color: #999999;
}
</style>