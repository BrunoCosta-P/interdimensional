<template>
  <div class="container-main" ref="inicio">
    <v-row justify="center" class="container-filter">
      <v-col>
        <v-text-field
          v-model="characterName"
          label="Name"
          variant="underlined"
        />
      </v-col>
      <v-col>
        <v-select
          v-model="status"
          label="Status"
          :items="listaStatus"
          variant="underlined"
        />
      </v-col>
    </v-row>
    <v-row class="grid-personagens">
      <baseComponents-card
        v-for="personagem in characters"
        :key="personagem.name"
        :personagem="personagem"
        class="personagem"
        @location="openModal"
      />
    </v-row>
    <v-row class="pagination">
      <v-col>
        <v-pagination v-model="page" :length="totalPages" rounded="0" />
      </v-col>
    </v-row>

    <baseComponents-modal
      v-if="showModal"
      :planet="handleIdLocation"
      @close="close"
    />
  </div>
</template>

<script setup>
import api from "~/server/api";

const characters = ref([]);
const page = ref(1);
const totalPages = ref(1);
const listaStatus = ref(["Alive", "Dead", "Unknown"]);
const status = ref("");
const characterName = ref("");
const showModal = ref(false);
const idLocation = ref(1);

const fetchCharacters = async () =>
  await api
    .get(
      `character/?page=${page.value}&status=${status.value}&name=${characterName.value}`
    )
    .then((response) => {
      totalPages.value = response.data.info.pages;
      characters.value = response.data.results;
    });

onBeforeMount(fetchCharacters);

watch([characterName, status, page], fetchCharacters);

const handleIdLocation = computed(() => {
  return idLocation;
});

function openModal(id) {
  idLocation.value = Number(id);
  showModal.value = true;
}

function close() {
  showModal.value = false;
}
</script>

<style lang="scss" scoped>
.container-main {
  width: 100vw;
  height: min-content;
  background: red;
  padding: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  .container-filter {
    width: 50%;
  }
  .grid-personagens {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;

    .personagem {
      margin: 1rem;
    }
  }

  .pagination {
    width: 50%;
  }
}
</style>
