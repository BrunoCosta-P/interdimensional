<template>
  <div class="container">
    <v-row>
      <v-col>
        <v-img :src="personagem.image" />
      </v-col>
      <v-col>
        <v-row no-gutters>
          <p class=""></p>
          <v-col cols="3"> Name: </v-col>
          <v-col>
            <p>{{ personagem.name }}</p>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="3"> Status: </v-col>
          <v-col
            ><v-chip :color="setColor(personagem.status)">
              {{ personagem.status }}</v-chip
            ></v-col
          >
        </v-row>
        <v-row>
          <v-col cols="3"> Species: </v-col>
          <v-col>
            <p>{{ personagem.species }}</p>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="3"> Origin: </v-col>
          <v-col >
            <p @click="clickLocation(personagem.origin.url)" class="origin">
              {{ personagem.origin.name }}
            </p>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="auto"> Last location: </v-col>
          <v-col>
            <p @click="clickLocation(personagem.origin.url)" class="origin">
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
  else emit("location", null)
}

function setColor(status) {
  console.log(status);

  switch (status) {
    case "Dead":
      return "red";

    case "Alive":
      return "green";

    default:
      break;
  }
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

  .origin{
    color: blue;
    cursor: pointer;
  }
}
</style>
