<template>
  <div>
    <h3>My Items - loading: {{ loading }}:</h3>
    <Loader v-show="loading" />
    <!-- В вызов компонента Loader добавьте привязку v-s\ how -->
    <ul v-show="!loading">
      <!-- Добавьте v-show="!loading" -->
      <ItemComponent
        v-for="item in items"
        :key="item.id"
        :model="item"
        @select="onItemSelect"
      />
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import { ItemInterface } from "@/models/items/Item.interface";
import ItemComponent from "./children/Item.component.vue";
import Loader from "@/components/shares/Loader.component.vue";

export default defineComponent({
  components: {
    ItemComponent,
    Loader,
  },
  props: {
    items: {
      type: Array as PropType<ItemInterface[]>,
    },
    loading: {
      type: Boolean,
    },
  },
  emits: ['selectItem'],
   setup(props, { emit }) {
    const onItemSelect = (item: ItemInterface) => {
      // item.selected = !item.selected;
      // console.log("onItemSelect", item.id, item.selected);
      emit('selectItem', item)
    };
    return { onItemSelect };
  },
});
</script>

<style lang="scss">
ul {
  list-style-type: none;
  margin-block-start: 0;
  margin-block-end: 0;
  margin-inline-start: 0px;
  margin-inline-end: 0px;
  padding-inline-start: 0px;
}
</style>
