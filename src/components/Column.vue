<script>
import Cards from "./cards.vue";

export default {
    components: {
        Cards
    },

    props: {
        colonne: String,
        quetes: Array
    }
}
</script>

<template>
    <div class="col">
        <h2> {{ colonne }}</h2>
        <Cards v-for="quete in quetes" :key="quete.id" :quete="quete" 
        @select-quete="$emit('select-quete', quete)" @changer-statut="(quete, nouveauStatut) => $emit('changer-statut', quete, nouveauStatut)"
        @supprimer-quete="$emit('supprimer-quete', $event)"
        />
    </div>
</template>