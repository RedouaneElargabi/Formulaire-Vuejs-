<template>
    <div class="container">
        <form>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <h1>Déposer une plainte</h1>
                    <hr>
                    <div class="form-group">
                        <label for="email">Mail</label>
                        <input
                                type="text"
                                id="email"
                                class="form-control"
                                v-model="userData.email">     <!-- V-model permet d'associer ce champ de saisie à la propriéte email ligne 127 (une liaison de données) -->
                    </div>
                    <div class="form-group">
                        <label for="password">Mot de passe</label>
                        <input
                                type="password"
                                id="password"
                                class="form-control"
                                v-model.lazy="userData.password">  <!-- Lazy est un modificateur -->
                    </div>
                    <div class="form-group">
                        <label for="age">Age</label>
                        <input
                                type="number"
                                id="age"
                                class="form-control"
                                v-model="userData.age">     <!-- Association du champ age à l'objet userData -->
                    </div> 

                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 form-group">
                    <label for="message">Message</label><br>
                    <!-- Interpolation between <textarea>{{ test }}</textarea> doesn't work!-->
                    <textarea
                            id="message"
                            rows="5"
                            class="form-control"
                            v-model="message"></textarea>
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <div class="form-group">
                        <label for="sendmail">
                            <input
                                    type="checkbox"
                                    id="sendmail"
                                    value="SendMail"
                                    v-model="sendMail"> Envoyer le mail        
                        </label>
                        <label for="sendInfomail">
                            <input
                                    type="checkbox"
                                    id="sendInfomail"
                                    value="SendInfoMail"
                                    v-model="sendMail"> Envoyer l'Infomail
                        </label>
                    </div>

                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 form-group">
                    <label for="male">
                        <input
                                type="radio"
                                id="male"
                                value="Homme"
                                v-model="gender"> Homme
                    </label>
                    <label for="female">
                        <input
                                type="radio"
                                id="female"
                                value="Femme"
                                v-model="gender"> Femme
                    </label>
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3 from-group">
                    <label for="priority">Priorité</label>
                    <select
                            id="priority"
                            class="form-control"
                            v-model="selectedPropertie">
                        <option v-for="propertie in properties">{{ propertie }}</option> 
                    </select>
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <app-switch v-model="dataSwitch"></app-switch>
                </div>
            </div>
            <hr>
            <div class="row">
                <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                    <button
                            class="btn btn-primary"
                            @click.prevent="submitted">Soumettre !   <!-- Le prevent permet de ne pas envoyer de requetes au serveur -->
                    </button>
                </div>
            </div>
        </form>
        <hr>
        <div class="row" v-if="isSubmitted">  <!-- De base =false donc n'apparait pas -->
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <div class="panel panel-default">
                    <div class="panel-heading">
                        <h4>Vos informations</h4>
                    </div>
                    <div class="panel-body">
                        <p>Mail: {{ userData.email }}</p>
                        <p>Mot de passe : {{ userData.password }}</p>
                        <p>Age: {{ userData.age }}</p>
                        <p style="white-space: pre">Message: {{ message }}</p>     <!-- Le style permet de conserver la structure si il y a des saut à la lignes -->
                        <p><strong>Envoyé le mail ?</strong></p>
                        <ul>
                            <li v-for="item in sendMail">{{ item }}</li>
                        </ul>
                        <p>Sexe: {{ gender }}</p>
                        <p>Priorité: {{ selectedPropertie }}</p>
                        <p>Changé : {{ dataSwitch }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Switch from './Switch.vue';   // Importation du commutateur // 

    export default {
        data() {
            return {
                userData: {
                    email:'',
                    password:'',
                    age: 24
                },
                message: 'Ici...',
                sendMail: [],
                gender:'Homme',
                properties: ['Faible', 'Moyen', 'Elevé'],
                selectedPropertie: 'Elevé',
                dataSwitch: true,
                isSubmitted: false,
            }
        },
        methods: {
            submitted(){
                this.isSubmitted = true;
            }
        },
        components: {
            appSwitch: Switch
        }

    }
</script>

<style>

</style>




<!-- Le v-model pour les checkbox doit être le meme pour les differentes option afin qu'il soit envoyer au tableau 

    Pour les bouton type radio, le v-model est appliqué au <select> et non pas sur <option>

        Rappel =>  :selected="propertie == 'Medium'"  permet de mettre Medium par défaut si il n'y a aucune valeur par defaut dans les data

