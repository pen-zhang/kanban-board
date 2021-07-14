<template>
  <div class="col card bg-light ms-1 me-1 d-flex" style="width: 250px; height:fit-content;" v-if="!deleted">
    <div class="card-header bg-transparent border-light d-flex justify-content-between align-items-center">
      <span class="h4">{{ listTitle }}</span>
      <button class="btn btn-close btn-close-dark" @click="deleted=true" ></button>
    </div>

    <div class="list-group card-body p-1">
      <div :id="'list-'+columnId.toString()" class="list-group " ></div>
      <button class="list-group-item list-group-item-action list-group-item-light" @click="clickAddCard" v-if="!addCardButtonClicked">
        + Add a card
      </button>
      <div class="list-group-item p-1" v-else>
        <form>
          <input type="text" v-model="cardTitle" class="form-control mt-1 mb-1" placeholder="Enter a title for this card..."  />
          <button type="submit" class="btn btn-primary btn-sm me-2 mb-1" @click.prevent="newCard">Add Card</button>
          <button class="btn-close mb-1" @click="clickAddCard"></button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import Card from './Card.vue';

export default {
  name: 'Column',
  data: function() {
    return {
      cardTitle: '',
      addCardButtonClicked: false,
      deleted: false,
      
    };
  },
  props: ['listTitle', 'columnId'],
  components: {
  },
  methods: {
    clickAddCard: function() {
      this.addCardButtonClicked = !this.addCardButtonClicked;
    },
    newCard : function() {
      if (this.cardTitle === '') return;

      var CardClass = Vue.extend(Card);
      var card = new CardClass({
        propsData: {cardTitle: this.cardTitle}
      });
      card.$mount();
      document.getElementById('list-'+this.columnId.toString()).append(card.$el);
      this.cardTitle = '';
      this.addCardButtonClicked = !this.addCardButtonClicked;
    },
  },
};
</script>
