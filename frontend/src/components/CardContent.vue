<template>
  <div class="card" style="height: 100%">
    <div class="card-header bg-transparent border-light h4">{{ title }}</div>
    <div class="card-body">
      <label class="card-title h6" for="card-description">Description</label>
      <textarea
        ref="editArea"
        class="p-1 text-start"
        name="card-description"
        placeholder="Add a more detailed description..."
        style="width: 100%; resize: none;"
        rows="2"
        @focus="editDescription"
        @blur="cancelEditting"
      ></textarea>
      <button class="btn btn-primary align-middle" v-show="showSaveButton">Save</button>
      <button class="btn-close ms-2 align-middle" v-show="showSaveButton"></button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardContent',
  data: function() {
    return {
      showSaveButton: false,
    };
  },
  props: ['title'],
  methods: {
    editDescription() {
      const textAreaElement = this.$refs.editArea;
      textAreaElement.setAttribute('rows', 5);
      this.showSaveButton = true;
    },
    cancelEditting() {
      const textAreaElement = this.$refs.editArea;
      textAreaElement.setAttribute('rows', textAreaElement.value.split(/\r?\n|\r/).length);
      this.showSaveButton = false;
    },
  },
};
</script>
