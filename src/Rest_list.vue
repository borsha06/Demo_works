<template>
  <v-ons-page>
  <div class="tabbar tabbar--top tabbar--top-border">
  <label class="tabbar__item tabbar--top-border__item">
    <input type="radio" name="top-tabbar-b" checked="checked">

    <button class="tabbar__button tabbar--top-border__button">
     Restaurant List
    </button>
     </label>
</div>
                                    <ons-col width="100%">
                                  
    <div class="restaurant" v-for="res in rest_lists">
                                        
                                        <p>    {{ res.post_title }}
                                        </p>
                                    </div>
                                </ons-col>

  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import app from './App';
  import axios from 'axios'

  export default {
    data ()
    {
      return {
        rest_lists : {}
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
            axios.get('http://clients.itsd.com.bd/table-cartel/wp-json/Table-cartel/v1/get-rest-by-loc/'+ this.data.id +'/')
            .then((resp) => {
              this.rest_lists  = resp.data
              console.log('--------------------------------')

              console.log(this.rest_lists)
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
  .restaurant{
background: #fff;
width: 100%;
text-align: left;
padding: 5px 3px;
font-size: 15px;
border-top: 1px solid #dedede;
border-bottom: 1px solid #dedede;
border-right: 1px solid #fff;

}
</style>