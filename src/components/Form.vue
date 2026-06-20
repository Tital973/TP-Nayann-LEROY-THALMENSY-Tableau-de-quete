<template>
    <form class="formulaire"  @submit.prevent="$emit('submit-form')">
        <input type ="text" placeholder="Titre de la quête" v-model="queteform.titre">
        <input type ="text" placeholder="Description " v-model="queteform.description">
        <select v-model="queteform.difficulte">
            <option>Facile</option>
            <option>Moyenne</option>
            <option>Difficile</option>
        </select>
        <input type="text" placeholder="Récompense " v-model="queteform.recompense">
        <button>{{ queteModification ? "Mettre a jour" : "Ajouter" }}</button>
    </form>
</template>

<script>
    export default{
        props: {
            queteform: Object,
            queteModification: Object
        }
    }
</script>