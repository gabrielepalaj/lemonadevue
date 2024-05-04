<template>
  <div>
    <div class="logo-container" :class="{ 'hidden': !isHeaderVisible }">
      <router-link to="/" class="logo">LeMonde.fr</router-link>
    </div>
    <header class="header" :class="{ 'white-background': !isHeaderVisible }">
      <div class="container">
        <nav>
          <ul class="nav-links">
            <li class="dropdown" @click="toggleDropdown('user')">
              <a href="#">User</a>
              <div class="dropdown-menu" :class="{ 'show': isDropdownOpen.user }">
                <div class="menu-content">
                  <div class="menu-section">
                    <h3>Voci</h3>
                    <ul>
                      <li><a href="#">Link 1</a></li>
                      <li><a href="#">Link 2</a></li>
                      <li><a href="#">Link 3</a></li>
                      <!-- Aggiungi altri link qui -->
                    </ul>
                  </div>
                  <ArticleComponent v-for="article in articles" :key="article.id" :article="article" />
                </div>
              </div>
            </li>
          </ul>
        </nav>
        <div class="search">
          <input type="text" placeholder="Cerca...">
          <button>Cerca</button>
        </div>
        <div class="login-button">
          <a href="#">Accedi / Abbonati</a>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
import ArticleComponent from './ArticleComponent.vue';
export default {
  name: 'HeaderComponent',
  components: {
    ArticleComponent, // Registra il componente Header
  },
  data() {
    return {
      isDropdownOpen: {
        user: false
      },
      isHeaderVisible: true,
      articles: [
        { id: 1, title: 'Titolo Articolo 1', imageUrl: 'url_immagine_articolo_1' },
        { id: 2, title: 'Titolo Articolo 2', imageUrl: 'url_immagine_articolo_2' },
        { id: 3, title: 'Titolo Articolo 3', imageUrl: 'url_immagine_articolo_3' },
        { id: 4, title: 'Titolo Articolo 4', imageUrl: 'url_immagine_articolo_4' }
      ]
    };
  },
  methods: {
    toggleDropdown(menu) {
      this.isDropdownOpen[menu] = !this.isDropdownOpen[menu];
    },
    handleScroll() {
      this.isHeaderVisible = window.scrollY < 50; // Imposta visibilità del logo in base allo scroll
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  unmounted() {
    window.removeEventListener('scroll', this.handleScroll);
  }
}
</script>

<style scoped>
/* Stili CSS per l'header */
.logo-container {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background-color: #0056b3;
  padding: 10px 20px;
  color: #fff;
  z-index: 999;
  transition: transform 0.3s ease;
}

.logo {
  font-size: 24px;
  font-weight: bold;
  color: #fff;
  text-decoration: none;
}

.header {
  padding: 50px 0 10px;
}

.white-background {
  background-color: #fff;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.nav-links {
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links li {
  display: inline-block;
  margin-right: 20px;
}

.nav-links li:last-child {
  margin-right: 0;
}

.dropdown {
  position: relative;
}

.dropdown-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  width: 100vw; /* Largo quanto la pagina */
  background-color: #fff;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.show {
  display: block;
}

.menu-content {
  display: flex;
}

.menu-section, .article-section {
  flex: 1;
}

.menu-section h3, .article-section h3 {
  margin-bottom: 10px;
}

.menu-section ul {
  list-style: none;
  padding: 0;
}

.menu-section ul li {
  display: block;
  margin-bottom: 5px;
}

.search {
  margin-left: 20px;
}

.search input[type="text"] {
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

.search button {
  padding: 5px 10px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

.login-button {
  margin-left: 20px;
}

.hidden {
  display: none;
}
</style>