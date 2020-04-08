<template>
  <div id="app">

    <md-toolbar class="md-dark">
      <div class="md-toolbar-row">
        <div class="md-toolbar-section-start">
          <h3 class="md-title">CourseSurvey</h3>
        </div>
        <div class="md-toolbar-section-end">
          <md-button
            class="md-just-icon md-simple md-white md-toolbar-toggle"
          >
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </md-button>

          <div class="md-collapse">
            <md-list>
              <md-list-item href="javascript:void(0)">
                <i class="fab fa-facebook-square"></i>
                <p>Facebook</p>
              </md-list-item>

              <md-list-item href="javascript:void(0)">
                <i class="fab fa-twitter"></i>
                <p>Twitter</p>
              </md-list-item>

              <md-list-item href="javascript:void(0)">
                <i class="fab fa-instagram"></i>
                <p>Instagram</p>
              </md-list-item>

              <md-list-item href="/users">
                <i class="fab fa-instagram"></i>
                <p>Users</p>
              </md-list-item>
            </md-list>
          </div>
        </div>
      </div>
    </md-toolbar>

    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
