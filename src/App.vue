

<template>
<div class="content-apply">
    <div class="apply-addMovie">
        <span>Nouveau film</span><br />
        Title : <br /><input type="text" v-model="movie_to_add.title" /><br />
        affiche : <br /><input type="text" v-model="movie_to_add.affiche" /><br />
        Year : <br /><input type="text" v-model="movie_to_add.year" /><br />
        Synopsys : <br /><textarea v-model="movie_to_add.synopsys"></textarea><br />
        <button v-on:click="newmovie2">Add</button>
    </div>
    <input class="rechercheBar" type="text" v-model="search" placeholder="Search" /><p>Movie number : {{movies.length}}</p>

    <ul>
        <movie-item v-for="(movie, index) in movies_search" v-bind:key="movie.title" v-bind:movie="movie" v-on:edit="edit(movie)" v-on:note="addnote(movie)" v-on:remove="remove(index)"></movie-item>
    </ul>

    <div class="modal-edit" v-if="movie_to_edit">
        Modifier le film<br /><br />
        Title : <br/><input type="text" v-model="movie_to_edit.title" /><br />
        affiche : <br/><input type="text" v-model="movie_to_edit.affiche" /><br />
        Year : <br/><input type="text" v-model="movie_to_edit.year" /><br />
        Synopsys : <br/><textarea v-model="movie_to_edit.synopsys"></textarea><br />
        <button v-on:click="save">Save</button>
    </div>

    <p class="modal-edit" v-if="movie_to_notes">
        Note du film<br />
        note :
        <input type="numbre" id="inputnote" name="vote" v-model="movie_to_notes"><br />
        <button v-on:click="savenote">Save</button>
    </p>

</div>
</template>

<script>
export default {
    data() {
        return {
            movie_to_add: {},
            movie_to_edit: null,
            movie_to_notes: null,
            search: "",
            movies : [
                {
                    title: "Star Wars IV: un nouvel espoir",
                    affiche: "https://www.editions-delcourt.fr/images/couvertures/star-wars-episode-iv-un-nouvel-espoir.jpg",
                    year: 1977,
                    synopsys: "C'est une époque de guerre civile. À bord de vaisseaux spatiaux opérant à partir d'une base cachée, les rebelles ont emporté leur première victoire sur le maléfique Empire Galactique.</br>Au cours de la bataille, des espions rebelles ont réussi à dérober les plans secrets de l'arme absolue de l'Empire : l'Étoile de la Mort, une station spatiale blindée dotée d'un équipement assez puissant pour annihiler une planète tout entière.Poursuivie par des sbires sinistre de l'Empire, la princesse Leia file vers sa base dans son vaisseau cosmique, porteuse des plans volés à l'ennemi qui pourront sauver son peuple et restaurer la liberté dans la galaxie.... ",
                    notes: [3,1,4,1]
                },
                {
                    title:"jurassic park",
                    affiche: "https://vignette.wikia.nocookie.net/jurassicpark/images/c/ce/JP-MoviePoster.jpg/revision/latest?cb=20150703133444&path-prefix=fr",
                    year:1993,
                    note: [3,4,1],
                    synopsys:"Ne pas réveiller le chat qui dort, c'est ce que le milliardaire John Hammond aurait dû se rappeler avant de se lancer dans le clonage de dinosaures. C'est à partir d'une goutte de sang absorbée par un moustique fossilisé que John Hammond et son équipe ont réussi à faire renaître une dizaine d'espèces de dinosaures.",
                    notes: [3,1,4,5]
                },
                {
                    title:"Retour vers le futur",
                    affiche: "http://img.over-blog-kiwi.com/1/20/70/98/20170924/ob_ea4711_affiche-retour-vers-le-futur.jpg",
                    year:1985,
                    synopsys:"Le jeune Marty McFly mène une existence anonyme, auprès de sa petite amie Jennifer, seulement troublée par sa famille en crise et un proviseur qui serait ravi de l'expulser du lycée. Ami de l'excentrique professeur Emmett Brown, il l'accompagne tester sa nouvelle expérience : le voyage dans le temps via une DeLorean modifiée. La démonstration tourne mal : des trafiquants d'armes débarquent et assassinent le scientifique.",
                    notes: [3,1,1,1]
                }
            ]
        }
    },

    methods: {
        newmovie1: function() {
            this.movies.push({title:"New movie"})
        },
        newmovie2: function() {
            this.movies.push(this.movie_to_add)
            this.movie_to_add = {}
        },

        edit: function(movie) {
            this.movie_to_edit = movie
        },
        save: function() {
            this.movie_to_edit = null
        },
        remove: function(index) {
            this.movies.splice(index, 1)
        },
        addnote: function(movie){
          this.movie_to_notes = movie.notes
        },
        savenote: function(movie){
          this.movie_to_notes = null
        }
    },

    created: function() {
        console.log("Created")
    },

    computed: {
        firstletter: function() {
            return this.message[0]
        },
        movies_search: function() {
            return this.movies.filter(m => m.title.toLowerCase().indexOf(this.search.toLowerCase())!=-1);
        }
    }
}
</script>
