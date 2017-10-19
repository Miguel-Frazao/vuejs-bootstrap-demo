<template>
  <div id="app" v-cloak>
    <nav-bar v-bind:products_cart="products_cart" v-bind:len_users="users.length" ref="navBar"></nav-bar>
    <b-container fluid class="main-container">
      <router-view :key="$route.path" v-bind:users="users" v-bind:products_cart="products_cart"></router-view>
    </b-container>
  </div>
</template>
<script>
export default {
  name: 'app', 
  data() {
    return {
      users: JSON.parse(localStorage.getItem("users")) || [],
      products_cart: {total: 0, products: []},
    }
  },
  watch: {
    total_cart: function(new_val, old_val) {
      this.products_cart.total = new_val;
    }
  },
  computed: {
    total_cart: function() {
      return this.products_cart.products.reduce(function(sum, p) { 
        p.total = p.qtd * p.value;
        return sum + p.total;
      }, 0);
    }
  }
}
</script>

<style>
@import url('../node_modules/bootstrap/dist/css/bootstrap.css');
@import url('../node_modules/bootstrap-vue/dist/bootstrap-vue.css');
@import url(https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css);

[v-cloak] { display:none }

.inline-block {
  display: inline-block;
}
.no-padding {
  padding: 0;
}

.main-container {
  width: 100%;
  max-width: 1230px;
  padding-top: 80px;
  padding-bottom: 80px;
}
.card-image {
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  width: 100%;
  height: 180px;
}
.card_container * {
  color: #222222;
}
.card_container {
  margin: 8px 0;
}
.card_container:hover * {
  text-decoration: none;
}
.card-text.description {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.card {
  padding: 15px;
}
button {
  cursor: pointer;
}
</style>
