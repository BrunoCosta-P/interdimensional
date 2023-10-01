<template>
  <v-sheet class="mx-auto" elevation="8" max-width="800">
    <v-slide-group v-model="model" class="pa-4" show-arrows>
      <v-slide-group-item
        v-for="resident in handleResidents"
        :key="resident.id"
        v-slot="{ selectedClass }"
      >
        <v-card
          color="grey-lighten-1"
          :class="['ma-4', selectedClass]"
          height="200"
          width="100"
        >
          <v-img :src="resident.image" />
          <p>Name: {{ resident.name }}</p>
        </v-card>
      </v-slide-group-item>
    </v-slide-group>
  </v-sheet>
</template>

<script setup>
const props = defineProps(["character"]);

const characterData = ref([]);

const handleResidents = computed(() => {
  return props.character.value;
});
</script>

<style lang="scss" scoped>
.teste {
  flex-direction: column;
}
</style>
