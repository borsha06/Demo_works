<template>
  <v-ons-page>
    <custom-toolbar>Page 1</custom-toolbar>
    <p style="text-align: center">
      This is the first page
      <v-ons-button @click="push">Push Page 2</v-ons-button>
    </p>
    <div>
    <div class="background">
      <ons-row align="center">
        <ons-col width="80%">
       
                                            <div v-for="r in rest" >
                                                <ons-row>
                                                    <ons-col width="80%" align="left">
                                                        <div class="card__content" align="center">
                                                            <h4 >
                                                                 {{r.name}}
                                                            </h4>
                                                          </div>
                                                        </ons-col>
                                                      </ons-row>
                                                    </div>
                                                  </ons-col>
                                                </ons-row>
                                              </div>
                                            </div>
                                            

  </v-ons-page>
</template>

<script>
  import customToolbar from './CustomToolbar';
  import page2 from './Page2';
  import axios from 'axios'
  export default {
    data ()
    {
      return {
        rest : {}
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
       axios.get('http://clients.itsd.com.bd/table-cartel/wp-json/wp/v2/all-terms?term=location')
         .then((resp) => {
           this.rest= resp.data
            console.log('--------------------------------')
            console.log(resp.data)
           this.loading = false
         })
         .catch((err) => {
//           console.log(err)
         })
     },
       pop(){
         this.pageStack.pop();
       },
       push() {
         this.pageStack.push(page2);
       }
     },
     props: ['pageStack'],
     components: { customToolbar }
  }
</script>

