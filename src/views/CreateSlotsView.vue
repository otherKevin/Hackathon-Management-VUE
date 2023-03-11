<template>
  <hr />
  <div class="componenterinos">
    <div>
      <CreateGroup />
    </div>
    <div>
      <CreateSlots />
    </div>
  </div>
</template>

<script>
import CreateSlots from "@/components/CreateSlots.vue";
import CreateGroup from "@/components/CreateGroup.vue";
export default {
  components: {
    CreateSlots,
    CreateGroup,
  },
};
</script>

<style scoped>
.componenterinos {
  /* display: flex;
  justify-content: center;
  gap: 12%; */
}
</style>
