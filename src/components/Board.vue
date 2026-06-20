<script>
import Column from "./Column.vue";

export default {
    components: {
        Column
    },

    props: {
        colonnes: Array,
        quetes: Array
    }
}
</script>

<template>
    <div class="tab">
        <Column v-for="colonne in colonnes" :key="colonne" :colonne="colonne" :quetes="quetes.filter(q => q.statut === colonne)"
            @select-quete="$emit('select-quete', $event)" @changer-statut="(quete, nouveauStatut) => $emit('changer-statut', quete, nouveauStatut)"
            @supprimer-quete="$emit('supprimer-quete', $event)"
        />
    </div>
</template>