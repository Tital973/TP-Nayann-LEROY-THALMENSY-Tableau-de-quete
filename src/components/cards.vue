
<template>
    <div class="carte" :class="quete.difficulte" @click="$emit('select-quete',quete)">
        <h3>{{ quete.titre }}</h3>
        <p>{{ quete.description }}</p>
        <p>Difficulté : {{ quete.difficulte }}</p>
        <p>Récompense :{{ quete.recompense }}</p>
        <p v-if="quete.statut === 'Terminée'" class='badge'>Récompense récupérée ! 🏆</p>
        <div class="actions">
                <button v-if="quete.statut === 'Terminée' || quete.statut === 'Echouée'"  @click.stop="$emit('changer-statut', quete, 'Disponible')">Disponible</button>
                <button v-if="quete.statut === 'Disponible'" @click.stop="$emit('changer-statut', quete, 'En cours')">En cours</button>
                <button v-if="quete.statut === 'En cours'" @click.stop="$emit('changer-statut', quete, 'Terminée')">Terminée</button>
                <button v-if="quete.statut === 'En cours'" @click.stop="$emit('changer-statut', quete, 'Echouée')">Echouée</button>
                <button v-if="quete.statut !== 'Terminée'" @click.stop="$emit('supprimer-quete', quete.id)">Supprimer</button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        quete: Object
    }
}
</script>
