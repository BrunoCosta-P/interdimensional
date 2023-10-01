<template>
  <div class="container">
    <v-row>
      <v-col>
        <v-img :src="personagem.image" />
      </v-col>
      <v-col>
        <v-row no-gutters>
          <v-col> Name: {{ personagem.name }} </v-col>
        </v-row>
        <v-row>
          <v-col> Status: {{ personagem.status }} </v-col>
        </v-row>
        <v-row>
          <v-col> Species: {{ personagem.species }}</v-col>
        </v-row>
        <v-row>
          <v-col>
            Origin:
            <p @click="clickLocation(personagem.origin.url)">
              {{ personagem.origin.name }}
            </p>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            Last known location:
            <p @click="clickLocation(personagem.origin.url)">
              {{ personagem.location.name }}
            </p>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script setup>
const props = defineProps(["personagem"]);

const emit = defineEmits(["location"]);

function clickLocation(location) {
  const match = location.match(/\/(\d+)$/);

  if (match && match[1]) emit("location", match[1]);
}
</script>

<style lang="scss" scoped>
.container {
  width: 35rem;
  height: min-content;
  border: solid 1px green;
  padding: 0.5rem;
  border-radius: 0.5rem;
  background-color: #565553;
}
</style>
