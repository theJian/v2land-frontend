<template>
  <nuxt-link
    :class="[
      'subscribe-container',
      $route.name !== 'name-admit' || 'exact-active-link'
    ]"
    :to="{ name: 'name-admit', params: { name } }"
  >
    <span v-if="pendingNews" class="event-action-badge">{{ pendingNews }}</span>
    <span class="text light-font">审核队列</span>
    <i class="icon icon-event_available light-font" />
  </nuxt-link>
</template>

<script>
  export default {
    computed: {
      name() {
        return this.$route.params.name;
      },
      pendingNews() {
        return this.$store.getters.getPendingNews(this.name).length;
      },
    },
    created() {
      this.$store.dispatch('getPendingNews', this.$route.params.name);
    },
  };
</script>
