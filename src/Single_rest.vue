<template>
  <v-ons-page>
  <div class="tabbar tabbar--top tabbar--top-border">
  <label class="tabbar__item tabbar--top-border__item">
    <input type="radio" name="top-tabbar-b" checked="checked">

    <button class="tabbar__button tabbar--top-border__button">
     Restaurant 
    </button>
     </label>
</div>
                                    <ons-col width="100%">
                                  
    <div class="single_restaurant" >
                                        
                                         <h1 strong>  {{single_rest.post_title}} </strong> </h1>
                                        <div> 
                                        	<h5>Cuisine Type</h5>
                                        	<p  v-for="item in single_rest.cuisine_type" >
                                            {{ item.name }}
                                        </p>
                                    </div>
                                    <div>
                                    	<h4> Address </h4>
                                    	<p>{{single_rest.restaurant_address}} </p>

                                </div>
	                                <div> 
	                                	<h4> Ratings </h4>
									<p> {{single_rest.restaurant_rating}} </p>
                                </div>
                                <div>
                                 <img :src="single_rest.restaurant_logo"/>
                                </div>


                                </div>
                                </ons-col>

  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import app from './App';
  import axios from 'axios'

  export default {
  	name :'singlerest',
    data ()
    {
      return {
        single_rest : {}
      }
    },
     created () {
            this.fetchData()
        },
        watch: {
            '$route': 'fetchData'
        },
        methods: {
          fetchData () {
            this.loading= true
            axios.get('http://clients.itsd.com.bd/table-cartel/wp-json/Table-cartel/v1/get-single-rest/'+ this.data.id +'/')
            .then((resp) => {
              this.single_rest = resp.data
              console.log('--------------------------------')

              console.log(this.single_rest)
              this.loading = false
          })
          .catch((err) => {
//           console.log(err)
          })
      },
     
           
        pop(){
         this.pageStack.pop();
       },
     },

    props: ['pageStack'],
    components: { customToolbar }
  }
</script>
<style>
.single_restaurant
{
    background: #fff;
    width: 100%;
    text-align: left;
    padding: 0px 5px;
    font-size: 15px;
    border-right: 1px solid #fff;



}
</style>














  