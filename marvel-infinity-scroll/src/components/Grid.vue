<template>
    <div class="flex-grid" ng-if="comics">
        <GridItem v-for="item in comics" :key="item.id" :comic="item"/>
    </div>
</template>

<script>
import GridItem from "./GridItem.vue";

export default {
  props: ["comics"],
  components: {GridItem},
};
</script>

<style scoped>
@media (max-width: 400px) {
  .flex-grid {
    display: block;
  }
}

.flex-grid {
  display: flex;
}
.col {
  flex: 1;
}

.flex-grid-thirds {
  display: flex;
  justify-content: space-between;
}
.flex-grid-thirds .col {
  width: 32%;
}
</style>
