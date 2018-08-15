<template>
    <div class="grid" ng-if="comics">
        <GridItem  v-for="item in comics" :key="item.id" :comic="item"/>
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

</style>
