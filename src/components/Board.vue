<template>
  <div>
    <header>
      Vue2 Trello
    </header>
    <main>
      <p class="info-line">All: {{ totalCardCount }} tasks</p>
      <draggable 
        :list="lists"
        @end="movingList"
        class="list-index"
      >
        <list 
          v-for="(item, index) in lists"
          :key="item.id"
          :title="item.title"
          :cards="item.cards"
          :listIndex="index"
          @change="movingCard"
        />
        <list-add/>
      </draggable>
    </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import List from './List'
import ListAdd from './ListAdd'
import { mapState } from 'vuex'

export default {
  components: {
    ListAdd,
    List,
    draggable
  },
  computed: {
    ...mapState([
      'lists'
    ]),
    totalCardCount() {
      return this.$store.getters.totalCardCount
    }
  },
  methods: {
    movingCard: function() {
      this.$store.dispatch('updateListAction', { lists: this.lists })
    },
    movingList: function() {
      this.$store.dispatch('updateListAction', { lists: this.lists })
    }
  }
}
</script>
