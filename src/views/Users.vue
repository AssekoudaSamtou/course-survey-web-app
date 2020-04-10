<template>
  <div class="about">
    <h1>This is the users page</h1>

    <div>
      <md-table v-model="searched" md-sort="name" md-sort-order="asc" md-card md-fixed-header>
        <md-table-toolbar>
          <div class="md-toolbar-section-start">
            <h1 class="md-title">Users</h1>
            <md-button class="md-dense md-raised md-primary" @click="showDialog = true">Ajouter</md-button>
          </div>

          <md-field md-clearable class="md-toolbar-section-end">
            <md-input placeholder="Search by name..." v-model="search" @input="searchOnTable" />
          </md-field>
      </md-table-toolbar>

        <md-table-empty-state
          md-label="No users found"
          :md-description="`No user found for this '${search}' query. Try a different search term or create a new user.`">
          <md-button class="md-primary md-raised" @click="newUser">Create New User</md-button>
        </md-table-empty-state>

        <md-table-row slot="md-table-row" slot-scope="{ item }" @click="updateUser(item)">
          <md-table-cell md-label="ID" md-sort-by="id" md-numeric>{{ item.id }}</md-table-cell>
          <md-table-cell md-label="Nom" md-sort-by="nom">{{ item.nom }}</md-table-cell>
          <md-table-cell md-label="Prénom" md-sort-by="prenom">{{ item.prenom }}</md-table-cell>
          <md-table-cell md-label="Email" md-sort-by="email">{{ item.email }}</md-table-cell>
          <md-table-cell md-label="Téléphone" md-sort-by="telephone">{{ item.telephone }}</md-table-cell>
          <md-table-cell md-label="Genre" md-sort-by="genre">
            <span v-if="item.genre === 'M'">Masculin</span>
            <span v-else-if="item.genre === 'F'">Féminin</span>
          </md-table-cell>
          <md-table-cell md-label="Titre" md-sort-by="titre">{{ item.titre }}</md-table-cell>
        </md-table-row>
      </md-table>
    </div>

    <div>
      <md-dialog :md-active.sync="showDialog">
        <md-dialog-title>{{ dialogTitle }}</md-dialog-title>

        <md-field>
          <label>Nom</label>
          <md-input v-model="user.nom" placeholder="Jonh"></md-input>
        </md-field>

        <md-field>
          <label>Prénom</label>
          <md-input v-model="user.prenom" placeholder="Doe"></md-input>
        </md-field>

        <md-field>
          <label for="type">Genre</label>
              <md-select v-model="user.genre" name="genre" id="genre">
                <md-option value="M">Masculin</md-option>
                <md-option value="F">Féminin</md-option>
              </md-select>
        </md-field>

        <md-field>
          <label>Email</label>
          <md-input v-model="user.email" placeholder="jonhdoe@example.com"></md-input>
        </md-field>

        <md-field>
          <label>Téléphone</label>
          <md-input v-model="user.telephone" placeholder="+228 98 65 32 54"></md-input>
        </md-field>

        <div class="md-layout md-gutter">
          <div class="md-layout-item">
            <md-field>
              <label for="type">Titre</label>
              <md-select v-model="user.titre" name="titre" id="titre">
                <md-option value="Enseignant">Enseignant</md-option>
                <md-option value="Etudiant">Etudiant</md-option>
                <md-option value="Admin">Administrateur</md-option>
              </md-select>
            </md-field>
          </div>
        </div>

        <md-dialog-actions>
          <md-button class="md-primary" @click="showDialog = false">Close</md-button>
          <md-button v-show="showSaveBtn" class="md-primary" @click="newUser()">Save</md-button>
        </md-dialog-actions>
      </md-dialog>
    </div>
  </div>
</template>
<script>
  const toLower = text => {
    return text.toString().toLowerCase()
  };

  const searchByName = (items, term) => {
    if (term) {
      return items.filter(item => toLower(item.name).includes(toLower(term)))
    }

    return items
  };

  export default {
    name: 'TableSearch',
    data: () => ({
      search: null,
      showDialog: false,
      showSaveBtn: true,
      dialogTitle: "Ajout d'utilisateur",
      searched: [],
      user: {
        id : 0,
        nom: "",
        prenom: "",
        email: "",
        telephone: "",
        genre: "",
        titre: "",
      },
      users: [
        {
          id: 1,
          nom: "Shawna ",
          prenom: "Dubbin",
          email: "sdubbin0@geocities.com",
          telephone: "+228 87 54 21 69",
          genre: "M",
          titre: "Etudiant"
        }
      ]
    }),
    methods: {
      newUser () {
        this.users.push(this.user);
        this.user =  {
          id : 0,
          nom: "",
          prenom: "",
          email: "",
          telephone: "",
          genre: "",
          titre: "",
        };
        this.showDialog = false;

      },
      updateUser (item) {
        this.dialogTitle = "Modification d'utilisateur";
        this.showDialog = true;
        this.user = item;
        this.showSaveBtn = false;
      },
      searchOnTable () {
        this.searched = searchByName(this.users, this.search)
      }
    },
    created () {
      this.searched = this.users
    }
  }
</script>

<style lang="scss" scoped>
  .md-field {
    max-width: 300px;
  }
</style>
