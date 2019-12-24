<template>
    <div>
        <h5>{{ title }} <span class="badge badge-info">{{ items.length }}</span></h5>
        <div class="card">
            <div class="card-body">
                <ul class="list-group">
                    <li class="list-group-item" v-for="item in items" v-bind:key="item">
                        <div class="row">
                            <div class="col-md">
                                {{ item }}
                            </div>
                            <div class="col-md text-right">
                                <button class="btn btn-sm btn-danger" v-on:click="deleteItem(item)"><i class="fa fa-trash"></i></button>
                            </div>
                        </div>
                    </li>
                    <br>
                    <div class="input-group">
                        <input type="text" class="form-control" v-model="item" v-on:keyup.enter="addItem(item)" placeholder="Digite o item">
                        <div class="input-group-append">
                            <button class="btn btn-info" v-on:click="addItem(item)"><i class="fa fa-plus"></i></button>
                        </div>
                    </div>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'AppItemList',
  props: ["items", "title"],
  data() {
      return {
          item: ""
      };
  },
  methods: {
      addItem(item) {
          this.item = "";
          this.$emit('addItem', item);
      },
      deleteItem(item) {
          this.$emit('deleteItem', item);
      }
  }
}
</script>

<style>

</style>
