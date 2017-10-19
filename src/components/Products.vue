<template>
  	<b-row class="products">
	  	<b-col lg="3" md="6" class="text-center card_container" v-for="prod in products" :key="prod.id">
	  		<router-link :to="'product/' +prod.id">
		  		<div class="card" style="width: 100%;">
		  			<div class="card-image" :style="'background-image: url(' +prod.picture+ ')'"></div>
					<div class="card-block">
						<h4 class="card-title">{{prod.name}}</h4>
						<p class="card-text description">{{prod.description}}</p>
						<div class="actions">
							<b-button v-if="prod_in_cart(prod)" disabled>On Cart</b-button>
				  			<b-button v-else variant="success" v-on:click.prevent="add_to_cart(prod)"><span class="fa fa-shopping-cart"></span></b-button>
						</div>
					</div>
				</div>
			</router-link>
	  	</b-col>
	</b-row>
</template>
<script>
export default {
	props: ['products_cart'],
	data() {
		return {
			sort_dir: '',
			products: [
				{
					id: 1,
					name: 'Eagle',
					value: 100,
					picture: 'https://images.pexels.com/photos/133356/pexels-photo-133356.jpeg',
					description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, nostrum odio. Dolores, sed accusantium quasi non, voluptas eius illo quas, saepe voluptate pariatur in deleniti minus sint. Excepturi.',
				},
				{
					id: 2,
					name: 'Duck',
					value: 200,
					picture: 'https://images.pexels.com/photos/255416/pexels-photo-255416.jpeg',
					description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, ',
				},
				{
					id: 3,
					name: 'Parrot',
					value: 300,
					picture: 'https://image.freepik.com/free-photo/parrot-jpg_21160030.jpg',
					description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, llo quas, saepe voluptate pariatur in deleniti minus sint. Excepturi',
				},
				{
					id: 4,
					name: 'Seagull',
					value: 400,
					picture: 'https://i.pinimg.com/originals/e0/63/8c/e0638cc91d2e6302608cd5f899e83529.jpg',
					description: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, ',
				},
			]
		}
	},
	methods: {
		prod_in_cart: function(prod) {
			return this.products_cart.products.findIndex((p, idx) => p.id == prod.id) !== -1;
		},
		add_to_cart: function(prod) {
			// NOTE: DO NOT this.products_cart.products.push(prod) ... THIS WILL GENERATE A CONFLIT BECAUSE products_cart AND products WILL SHARE THE SAME DEEP OBJECT (SAME MEMORY SPACE)
			this.products_cart.products.push({picture: prod.picture, id: prod.id, value: prod.value, qtd: 1, name: prod.name});
		},
		sort_price: function() {
			if(this.sort_dir == 'up') {
				this.products.sort(function(a, b) { return a.value - b.value});
			}
			else {
				this.products.sort(function(a, b) { return b.value - a.value});
			}
		}
	}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.actions span.fa {
		color: #ffffff;
	}
</style>