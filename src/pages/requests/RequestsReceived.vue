<template>
  <section>
    <base-dialog
      :show="!!error"
      :title="'An error occurred!'"
      @close="handleError"
    >
      <p>{{ error }}</p>
    </base-dialog>
    <base-card>
      <header>
        <h2>Requests received</h2>
      </header>
      <div v-if="isLoading">
        <base-spinner></base-spinner>
      </div>
      <ul v-else-if="hasRequests && !isLoading">
        <requested-item
          v-for="req in receivedRequests"
          :key="req"
          :email="req.userEmail"
          :message="req.message"
        >
        </requested-item>
      </ul>
      <h3 v-else>You havent received any requests yet.</h3>
    </base-card>
  </section>
</template>

<script>
import RequestedItem from '../../components/requests/RequestItem.vue';
export default {
  data() {
    return {
      isLoading: false,
      error: '',
    };
  },
  components: { RequestedItem },
  computed: {
    receivedRequests() {
      return this.$store.getters['requests/requests'];
    },
    hasRequests() {
      return this.$store.getters['requests/hasRequests'];
    },
  },
  created() {
    this.loadRequests()
  },
  methods: {
    async loadRequests() {
      this.isLoading = true;
      try {
        await this.$store.dispatch('requests/fetchRequests');
      } catch (error) {
        this.error = error.message || 'Something failed!';
      }
      this.isLoading = false;
    },
    handleError() {
      this.error = null;
    },
  },
};
</script>

<style scoped>
header {
  text-align: center;
}

ul {
  list-style: none;
  margin: 2rem auto;
  padding: 0;
  max-width: 30rem;
}

h3 {
  text-align: center;
}
</style>
