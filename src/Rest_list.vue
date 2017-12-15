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
                                  
    <div class="location_button" v-for="res in rest_lists">
                                        <button  @click="single_rest(res.ID)">
                                          {{ res.post_title }}
                                      </button>
                                    </div>
                                </ons-col>

  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import app from './App';
  import axios from 'axios'
  import single_rest from './Single_rest';

  export default {
    name :'restaurant_list',
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
              //console.log('--------------------------------')

              //console.log(this.rest_lists)
              this.loading = false
          })
          .catch((err) => {
//           console.log(err)
          })
      },
        single_rest(id) {
            this.pageStack.push({
                extends: single_rest,
                   data() {
                      return {
                          data: {'id': id}
                        }
                    }
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
.location_button{}
  .location_button{
    background: #fff;
    width: 100%;
    text-align: left;
    padding: 4px 3px;
    font-size: 15px;
    border-right: 1px solid #fff;
    border-bottom: bisque;
  }
.location_button button:hover{
  background:#ddd;

}

</style>