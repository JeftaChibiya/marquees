<template>
	<div>
		<!-- top controls -->
		<div class="container">
			<div class="level">
				<div class="level-left">
					<div class="level-item">
						<router-link to="/catalog">
							<a>
								<span class="icon">
								<i class="fa fa-angle-double-left"></i>
								</span> <span>Back</span>
							</a>						
						</router-link>
					</div>
				</div>
			</div>		
		 </div>

		<!-- page title -->
		<div class="original notice">
		  <div class="container">
		  	<div class="columns">
		  		<div class="column is-4 is-offset-4">
				  <p class="title is-3 white"><b>Add Product</b></p>		  			
		  		</div>
		  	</div>
		  </div>
		</div>
		
		<!-- content / purpose -->
	  	  <div class="container">
			<div class="columns">		
				<div class="column is-4 is-offset-4">
					<form method="POST" @submit.prevent="onSubmit" @keydown="form.errors.clear()">

						<p class="subtitle"><b>Name & Description</b></p>
						<div class="field">
							<label>Name:</label>
							<input type="text" class="input" v-model="form.name">
						</div>
						
						<p class="subtitle"><b>Measurements & Sizes</b></p>
						<div class="field is-grouped">
							<div class="field-body">
							  <div class="field">
								<label>Span:</label>
								<input type="text" class="input" v-model="form.span">
							  </div>
							  <div class="field">
								<label>Length:</label>
								<input type="text" class="input" v-model="form.length">
							  </div>							
							</div>
						</div>	

						<p class="subtitle"><b>Category or Types</b></p>									
						<div class="field">
						  <label>Category:</label>					
						  <div class="control">
						    <div class="select">

							  <select v-model="form.category">
						        <option>Select Category</option>
						        <option v-for="category in categories" :value="category.id">
						        	{{ category.name }}
						        </option>
							  </select>					      
							</div>
						  </div>
						</div>

						<p class="subtitle"><b>Attach Images</b></p>				
							
						<div class="field notification">
							<p class="subtitle is-6">
								Product images are presently added after the product has been created. 
								<b>Visit Catalog > product > edit</b> to Add images for this product
							</p>	
						</div>
					
						<div class="field">
							<button class="button is-light" :disabled="form.errors.any()">
								CREATE
							</button>
						</div>											
					</form>
				</div>
			</div>		
		</div>		
	</div>
</template>

<script>

import Category from '../models/Category';
import Dropzone from 'vue2-dropzone';

export default {

	components: { Dropzone },

	data() {
		return {
			categories: [],
			showUpload: false,
			csrfHeader: null,						
	        form: new Form({
	          name: '',
	          span: '',          
	          length: '',
	          category: ''
	        })
		}
	},
    created(){
      
        Category.all(categories => this.categories = categories);

        // this.csrfHeader = {
        // 	'X-CSRF-TOKEN': window.Marquees.csrfToken
        // }        

    },
	methods: {
		onSubmit() {
	        this.form
	          .post('/products')
	          .then(
	          	product => this.data === product,
				this.$router.push('catalog')	
	         );
		}
	},
    mounted() {
      
      // console.log(this.attributes.id)

    }	
}	
</script>