<template>
	<b-row class="cart">
		<b-col class="no-padding">
			<b-col cols="12">
				<h2>Total price: {{products_cart.total}} €</h2>
			</b-col>
	  		<b-col cols="12">
	  			<div>
				    <b-table :items="products_cart.products" :fields="fields">
				        <template slot="picture" scope="data">
					    	<img class="table-image" :src="data.value">
					    </template>
					    <template slot="actions" scope="data">
					    	<button class="btn btn-success" v-b-tooltip.hover.top title="More quantity" v-on:click="change_qtd(data.item, true)"><span class="fa fa-plus"></span></button>
					    	<button class="btn btn-warning" v-b-tooltip.hover.top title="Less quantity" v-on:click="change_qtd(data.item, false)"><span class="fa fa-minus"></span></button>
					    	<button class="btn btn-danger" v-b-tooltip.hover.top title="Remove from cart" v-on:click="open_modal(data.item)"><span class="fa fa-times"></span></button>
					    </template>
				    </b-table>
					<modal v-if="showModal" v-on:close="showModal = false">
						<h5 slot="header">Delete {{modal_item.name}} from cart?</h5>
						<div slot="footer">
							<b-button variant="danger" v-on:click="remove_from_cart(modal_item)">
								Yes
							</b-button>
							<b-button variant="default" v-on:click="showModal = false">
								Cancel
							</b-button>
						</div>
					</modal>
				</div>
	  		</b-col>
	  	</b-col>
	</b-row>
</template>

<script>
export default {
	props: ['products_cart'],
	data() {
		return {
    		showModal: false,
    		modal_product: {},
			fields: [
				{	
					key: 'picture',
					label: 'Picture',
					sortable: false,
					
				},
				{
					key: 'name',
					label: 'Name',
					sortable: true
				},
				{
					key: 'qtd',
					label: 'Quantity',
					sortable: true
				},
				{
					key: 'total',
					label: 'Total',
					sortable: true
				},
				/*{
					key: 'total_price',
					label: 'Total',
					sortable: true,
					formatter: (value, key, item) => {
						console.log(value);
						console.log(key);
						console.log(item);
						return item.qtd * item.value;
						
					}
				},*/
				{
					key: 'actions',
					label: 'Actions'
				}
		    ],
		}
	},
	methods: {
		remove_from_cart: function(product) {
			var prod_idx = this.products_cart.products.findIndex((prod, idx) => prod.id == product.id);
			this.products_cart.products.splice(prod_idx, 1);
			this.showModal = false;
		},
		change_qtd: function(prod, up) {
			if(up) {
				prod.qtd += 1;
			}
			else if(prod.qtd > 1) {
				prod.qtd -= 1;
			}
		},
		open_modal: function(prod) {
			this.modal_item = prod;
			this.showModal = true;
		},
	},
}
</script>
<style scoped>
	.modal-header h5 {
		margin: 0;
	}
	.table-image {
		max-height: 100px;
	}
</style>