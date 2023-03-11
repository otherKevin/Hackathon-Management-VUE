<template>
  <hr />
  <div class="eventSelect">
    <SelectEvent />
  </div>
</template>

<script>
import SelectEvent from "@/components/SelectEvent.vue";

export default {
  components: {
    SelectEvent,
  },
};
</script>

<style scoped>
.eventSelect {
  inline-size: 100%;
  align-items: center;
  justify-content: center;
  display: flex;
  flex-direction: column;
}
</style>
