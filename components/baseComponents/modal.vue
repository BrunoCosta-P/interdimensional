<template>
  <v-overlay v-model="overlay" class="overlay">
    <v-container class="container">
      <v-row>
        <v-col>
          <v-img src="@/assests\img\Rick_planet.jpg" />
        </v-col>
      </v-row>
      <v-row>
        <v-col>Name: {{ location.name }}</v-col>
        <v-col>Type: {{ location.type }}</v-col>
        <v-col>Dimension: {{ location.dimension }}</v-col>
      </v-row>
      <v-row>
        <v-col>
          <baseComponents-carousel :character="handleResidents" />
        </v-col>
      </v-row>
      <v-btn
        icon="$close"
        variant="text"
        class="btn-close"
        @click="buttonClick"
      />
    </v-container>
  </v-overlay>
</template>

<script setup>
import api from "~/server/api";
const props = defineProps(["planet"]);

const overlay = ref(true);
const idLocation = ref(props.planet.value);
const idResidents = ref([]);
const location = ref({});
const residents = ref([]);

const emit = defineEmits(["close"]);

const fetchLocation = async () =>
  await api.get(`location/${idLocation.value}`).then((response) => {
    const resp = response.data;
    location.value = {
      dimension: resp.dimension,
      type: resp.type,
      name: resp.name,
    };
    idResidents.value = setIdsResidents(resp.residents);

    fetchCharacter();
  });

const fetchCharacter = async () =>
  await api.get(`character/${idResidents.value}`).then((response) => {
    const resp = response.data;
    residents.value = resp;
  });

function setIdsResidents(residents) {
  return residents.map((residents) => {
    if (typeof residents === "string") {
      const match = residents.match(/\/(\d+)$/);

      if (match && match[1]) {
        return parseInt(match[1]);
      }
    }

    return null;
  });
}

function buttonClick() {
  emit("close");
}

const handleResidents = computed(() => {
  return residents;
});

onBeforeMount(fetchLocation);
</script>

<style lang="scss" scoped>
.overlay {
  display: flex;
  justify-content: center;
  align-items: center;

  .container {
    background: red;
    width: 50vw;
    min-height: 90vh;
    height: fit-content;
    position: relative;
    .btn-close {
      position: absolute;
      top: 0;
      right: 0;
    }
  }
}
</style>
