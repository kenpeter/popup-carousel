<template>
  <div id="app">
    <div>
      <!-- click, set var -->
      <button
        type="button"
        class="btn"
        @click="showModal"
      >
        Open Modal!
      </button>

      <!-- v show if -->
      <!-- click, set var -->
      <PopUp
        v-show="isModalVisible"
        @close="closeModal"
      />
    </div>
  </div>
</template>

<script>
import PopUp from './components/PopUp.vue'

export default {
  name: 'app',
  components: {
    PopUp
  },
  // data: later method changes
  data () {
    return {
      isModalVisible: false,
    };
  },
  // method list
  methods: {
    // make visible true
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      // make visible false
      this.isModalVisible = false;
    }
  },
}
</script>
