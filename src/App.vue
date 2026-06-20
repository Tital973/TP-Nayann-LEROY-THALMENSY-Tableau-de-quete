<script>
import Board from "./components/Board.vue";
import Questform from "./components/Form.vue";

export default{
  components: {
    Board,
    Questform
  },
  data(){
    return{
      colonnes:[
        "Disponible",
        "En cours",
        "Terminée",
        "Echouée"
      ],
      quetes : [
        {
          id:1,
          titre: "Chasser les goblins",
          description :"Tue 10 goblins", 
          difficulte : "Facile",
          recompense: "100 XP",
          statut: "Disponible"
        },
        {
          id:2,
          titre: "Chasser les loups",
          description :"Tue 20 loups", 
          difficulte : "Facile",
          recompense: "150 XP",
          statut: "Disponible"
        }
      ],
      nouvelleQuete:{
        titre:"",
        description:"",
        difficulte:"Facile",
        recompense:""
      },
      compteur: 3,
      queteModification: null
    }
  },
  methods:{
    ajouterQuete(){
      if(this.nouvelleQuete.titre ===""){
        alert("le titre est obligatoire");
        return;
      }
      if(this.queteModification){
        this.queteModification.titre = this.nouvelleQuete.titre;
        this.queteModification.description = this.nouvelleQuete.description;
        this.queteModification.difficulte = this.nouvelleQuete.difficulte;
        this.queteModification.recompense = this.nouvelleQuete.recompense;
        this.queteModification= null;
        this.nouvelleQuete = {
          titre: "",
          description: "",
          difficulte: "Facile",
          recompense: ""
        }
      }
      else{
        this.quetes.push(
          {
            id:this.compteur,
            titre: this.nouvelleQuete.titre,
            description : this.nouvelleQuete.description,
            difficulte: this.nouvelleQuete.difficulte,
            recompense: this.nouvelleQuete.recompense,
            statut: "Disponible"
          }
        );
        this.nouvelleQuete = {
          titre: "",
          description: "",
          difficulte: "Facile",
          recompense: ""
        }
        this.compteur++;
      }
    },
    changerStatut(quete, nouveauStatut){
      quete.statut= nouveauStatut;
    },
    supprimerQuete(id){
      this.quetes = this.quetes.filter(quete => quete.id !==id);
    },
    selectQuete(quete){
      this.queteModification = quete;

      this.nouvelleQuete={
        titre: quete.titre,
        description : quete.description,
        difficulte: quete.difficulte,
        recompense: quete.recompense
      };
    }
  },
  mounted() {
    const quetesSauvegardees= localStorage.getItem("quetes");
    if (quetesSauvegardees){
      this.quetes= JSON.parse(quetesSauvegardees);
    }
  },
  watch: {
    quetes:{
      handler(nouvellesQuetes){
        localStorage.setItem("quetes",JSON.stringify(nouvellesQuetes));
    },
    deep: true
  }
}
}
</script>

<template>
  <div class="app">
    <h1>⚔️ Tableau des Quêtes</h1>

    <Questform :queteform="nouvelleQuete" :quete-modification="queteModification" @submit-form="ajouterQuete"/>
    
    <Board :colonnes='colonnes' :quetes="quetes" @select-quete="selectQuete" @changer-statut="changerStatut" 
    @supprimer-quete="supprimerQuete"
    />  
  </div>
</template>

<style>

body {
  margin: 0;
  font-family: Georgia, "Times New Roman", serif;
  background:
    radial-gradient(circle at top, rgba(120, 80, 30, 0.25), transparent 35%),
    linear-gradient(135deg, #11110f, #24170f 45%, #0d0d0c);
  color: #ead8a6;
}

.app {
  min-height: 100vh;
  padding: 32px;
}

h1 {
  text-align: center;
  font-size: 44px;
  letter-spacing: 2px;
  color: #d8b15a;
  text-shadow: 2px 2px 0 #000, 0 0 18px #8b5a1f;
  margin-bottom: 32px;
}

.formulaire {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  padding: 18px;
  margin-bottom: 32px;
  background: #1b1510;
  border: 3px solid #7c5a2b;
  border-radius: 6px;
  box-shadow:
    inset 0 0 20px #000,
    0 0 18px #000;
}

.formulaire input,
.formulaire select {
  padding: 11px;
  background: #e7d3a0;
  color: #1c1208;
  border: 2px solid #5a3b1a;
  border-radius: 4px;
  font-family: Georgia, "Times New Roman", serif;
  font-weight: bold;
}

button {
  cursor: pointer;
  padding: 9px 12px;
  border-radius: 4px;
  border: 2px solid #3d260f;
  background: linear-gradient(#b8893f, #6d3f16);
  color: #fff1c2;
  font-family: Georgia, "Times New Roman", serif;
  font-weight: bold;
  text-shadow: 1px 1px 0 #000;
  box-shadow: inset 0 1px 0 #e0bc72, 0 3px 0 #2b1607;
}

button:hover {
  background: linear-gradient(#d0a04e, #7d4618);
  transform: translateY(-1px);
}

.tab {
  display: flex;
  gap: 18px;
  align-items: flex-start;
}

.col {
  flex: 1;
  min-height: 470px;
  padding: 14px;
  background:
    linear-gradient(180deg, #2a2118, #15110d);
  border: 3px solid #5d4523;
  border-radius: 8px;
  box-shadow:
    inset 0 0 25px #000,
    0 6px 18px #000;
}

.col h2 {
  white-space: nowrap;
  text-align: center;
  font-size: 21px;
  color: #d8b15a;
  padding-bottom: 12px;
  border-bottom: 2px solid #7c5a2b;
  text-shadow: 1px 1px 0 #000;
}

.carte {
  position: relative;
  margin-top: 16px;
  padding: 15px;
  background:
    linear-gradient(145deg, #d8c18a, #a98245);
  color: #211408;
  border: 2px solid #4a2c10;
  border-radius: 6px;
  box-shadow:
    inset 0 0 10px rgba(255, 240, 180, 0.35),
    0 5px 12px #000;
  transition: transform 0.2s, box-shadow 0.2s;
}

.carte:hover {
  transform: translateY(-4px);
  box-shadow:
    inset 0 0 12px rgba(255, 240, 180, 0.45),
    0 10px 18px #000;
}

.carte h3 {
  margin-top: 0;
  color: #3b1f0b;
  font-size: 22px;
  border-bottom: 1px solid rgba(70, 40, 10, 0.4);
  padding-bottom: 6px;
}

.carte p {
  font-size: 15px;
  line-height: 1.3;
}

.Facile {
  border-left: 8px solid #3f7d3a;
}

.Moyenne {
  border-left: 8px solid #b7832f;
}

.Difficile {
  border-left: 8px solid #8f1d1d;
}

.badge {
  background: #c9a348;
  color: #201205;
  border: 2px solid #5a3b1a;
  padding: 8px;
  border-radius: 4px;
  font-weight: bold;
  text-align: center;
  box-shadow: inset 0 0 8px #fff0a0;
}

.actions {
  display: flex;
  flex-wrap: wrap;
  gap: 7px;
  margin-top: 14px;
}

.actions button {
  font-size: 12px;
  padding: 6px 8px;
}

@media (max-width: 900px) {
  .tab {
    flex-direction: column;
  }

  .col {
    width: 100%;
  }

  .formulaire {
    flex-direction: column;
  }
}
</style>

