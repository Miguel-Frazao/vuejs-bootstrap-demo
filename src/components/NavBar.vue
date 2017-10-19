<template>
	<b-navbar toggleable="md" type="dark" variant="dark" fixed="top">
		<b-container fluid class="main-container nav">
			<b-nav-toggle target="nav_collapse"></b-nav-toggle>

			<b-navbar-brand href="#">Vuejs&Bootstrap</b-navbar-brand>

			<b-collapse is-nav id="nav_collapse">

				<b-nav is-nav-bar class="ml-auto">
					<b-nav-item to="/" exact><span class="fa fa-home"></span> Home</b-nav-item>
					<b-nav-item to="/users" exact><span class="fa fa-users"></span> Users <span class="badge badge-primary">{{len_users}}</span></b-nav-item>
					<b-nav-item to="/products" exact><span class="fa fa-cubes"></span> Products</b-nav-item>
					<b-nav-item to="/cart" exact><span class="fa fa-shopping-cart"></span> Cart <span class="badge badge-success">{{len_prods_cart}}</span></b-nav-item>
					<b-nav-item-dropdown right>
						<template slot="button-content">
							<em>Dropdown</em>
						</template>
						<b-dropdown-item to="#" exact>Dropdown1</b-dropdown-item>
						<b-dropdown-item to="#" exact>Dropdown2</b-dropdown-item>
						<b-dropdown-item to="#" exact>Just another dropdown</b-dropdown-item>
					</b-nav-item-dropdown>
					<b-nav-item to="/api" exact><span class="fa fa-code"></span> API</b-nav-item>
				</b-nav>

			</b-collapse>
		</b-container>
	</b-navbar>
</template>

<script>
export default {
	props: ['products_cart', 'len_users'],
	computed: {
		len_prods_cart: function() {
			return this.products_cart.products.length;
		},
	}
}
</script>
<style scoped>
	nav {
		padding: 8px 0;
	}
	.main-container.nav {
		padding: 0 15px;
	}
	.active {
		font-weight: bold;
	}
</style>
