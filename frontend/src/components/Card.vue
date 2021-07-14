<template>
  <button class="list-group-item list-group-item-action list-group-item-light mb-2 text-start" @click="showCardContent">
    <span>{{ cardTitle }}</span>
  </button>
</template>

<script>
import CardContent from './CardContent.vue';

export default {
  name: 'Card',
  data: function() {
    return {
    };
  },
  props: ['cardTitle'],
  methods: {
    showCardContent() {
      this.$modal.show(
        CardContent,
        { title: this.cardTitle},
        { name: 'card-details'
        },
        { 'before-open': ()=>{
            console.log('modal open');
          },
          'before-close': () => {
            console.log('modal closed');
          },
        }
      );
    },
  },
};
</script>
