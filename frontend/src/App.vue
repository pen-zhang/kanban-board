<template>
  <div
    id="app"
    class="container-fluid mt-3 align-items-start"
    style="height:100%; white-space: nowrap;"
  >
    <!-- Container for Lists -->
    <div id="columns" class="justify-content-start d-inline-flex"></div>
    <!-- Add New List Button -->
    <div
      class="card btn btn-light d-inline-block btn-outline-secondary "
      v-if="!addListButtonclicked"
      @click="clickAddList"
      style="width: 250px; height: 40px; margin-right: 1rem;  vertical-align: top;"
    >
      <span>
        + Add another list
      </span>
    </div>
    
    <div
      class="card d-inline-block bg-light btn-outline-secondary ps-1 pe-1"
      style="width: 250px; height: 85px; margin-right: 1rem;  vertical-align: top;"
      v-else
    >
      <form>
        <div>
          <input type="text" v-model="listTitle" class="form-control mt-1 mb-1" placeholder="Enter list title..." />
        </div>
        <button type="submit" class="btn btn-primary btn-sm me-2 mb-1" @click.prevent="newList">Add list</button>
        <button class="btn-close mb-1" @click="clickAddList"></button>
      </form>
    </div>
  </div>
</template>

<script>
import Column from './components/Column.vue';
import Vue from 'vue';

export default {
  name: 'App',
  components: {},
  data: function() {
    return {
      addListButtonclicked: false,
      listTitle: '',
      columnId: 0,
    };
  },
  methods: {
    clickAddList: function() {
      this.addListButtonclicked = !this.addListButtonclicked;
    },
    newList: function() {
      if (this.listTitle === '') return;

      var List = Vue.extend(Column);
      var list = new List({
        propsData: { listTitle: this.listTitle, columnId: this.columnId++ },
      });
      list.$mount();
      var columns = document.getElementById('columns');
      columns.appendChild(list.$el);
      this.listTitle = '';
      this.addListButtonclicked = !this.addListButtonclicked;
    },
  },
};
</script>
