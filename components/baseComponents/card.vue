<template>
  <div class="container">
    <v-row>
      <v-col>
        <v-img :src="personagem.image" />
      </v-col>
      <v-col>
        <v-row no-gutters>
          <v-col > Name: {{ personagem.name }} </v-col>
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
            <a :href="personagem.origin.url">{{ personagem.origin.name }}</a>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            Last known location:<a :href="personagem.location.url">
              {{ personagem.location.name }}</a
            >
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </div>
</template>

<script setup>
const props = defineProps(["personagem"]);
</script>

<style lang="scss" scoped>

.container{
  width: 35rem;
  height: min-content;
  border: solid 1px green;
  padding: .5rem;
  border-radius: .5rem;
  background-color: #565553;
}
</style>
