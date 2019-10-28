<template>
      <v-card class="overflow-hidden">
        <v-toolbar flat text app class="indigo"  dark height="57">
            <v-layout row wrap>
                <v-flex xs12 md12>
                <v-row justify="center" align="center">
                    <v-icon color="black" size="15" >mdi-map-marker</v-icon><span class="font-weight-bold subtitle-1">Quetzaltenango, quetzaltenango</span>
                </v-row>
                <v-row justify="center" align="center">
                    <v-icon color="black" size="15">mdi-calendar</v-icon><span class="font-weight-bold caption" >{{ this.days[new Date().getDay() ]}},{{ new Date().getDate()}} de {{  this.months[new Date().getMonth()] }} {{ new Date().getFullYear() }}</span>
                </v-row>
                </v-flex>
            </v-layout>
        </v-toolbar>
      <BottomNavigation/>
      <v-sheet class="overflow-y-auto indigo lighten-4" max-height="650">
      
      <v-container class="bottom" >
      <v-item-group v-model="selected" multiple> 
        <v-row justify="space-around">
          <v-col v-for="(company, i) in companies" :key="i" cols="12" md="4">
              <v-hover >
                <v-card  max="300" flat class="transparent" :elevation=12 >
                  <v-item v-slot:default="{ active, toggle }">
                    <v-img  :src="company.image" height="10em" class="text-right pa-2" @click="toggle"  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)">
                      <v-btn icon  text color="red accent-4" @click="toggle" :input-value="active">
                        <v-icon active-class="red accent-4"  @click="toggle" :input-value="active">
                          {{ active ? 'mdi-heart' : 'mdi-heart-outline' }}
                        </v-icon>
                      </v-btn>
                      <v-card-title class="title white--text">
                        <v-row class="fill-height flex-column" justify="space-between">
                          <div class="description">
                            <span class="mt-4  caption  text-left">{{ company.name }},</span>
                            <span class="mt-4  caption  text-left"> {{ company.address }}</span>
                            <v-divider inset vertical class="mx-1"></v-divider>
                            <span>
                              <v-icon size=18 color="amber accent-4">mdi-star</v-icon> 
                              <v-icon size=18 color="amber accent-4">mdi-star</v-icon>
                              <v-icon size=18 color="amber accent-4">mdi-star</v-icon>
                              <v-icon size=18 color="amber accent-4">mdi-star</v-icon>
                              <v-icon size=18 color="amber accent-4">mdi-star</v-icon>
                            </span>
                        </div>
                      </v-row>
                    </v-card-title>
                  </v-img>
                </v-item>
              <v-card-actions>
                <v-menu transition="scale-transition" origin="center center">
                  <template v-slot:activator="{ on }">
                    <v-btn block color="grey lighten-4"  v-on="on">
                      <span class="font-weight-bold">Contáctanos</span>
                    </v-btn>
                      </template>
                        <v-list class="grey lighten-4">
                          <v-list-item>
                            <v-row justify="center" align="center">
                              <div>
                                <v-list-item-title>
                                  <v-icon color="teal">mdi-email</v-icon>
                                  <span class="subtitle-2 font-weight-medium ">{{company.email}}</span>
                                </v-list-item-title>
                              </div>
                              <v-divider  vertical class="mx-2 ma-3"></v-divider>
                              <div>
                                <v-list-item-title>
                                  <v-icon  color="teal">mdi-phone</v-icon>
                                  <span class="subtitle-2 font-weight-medium ">{{company.phone}}</span>
                                </v-list-item-title>
                              </div>
                            </v-row>
                          </v-list-item>
                        </v-list>
                      </v-menu>
                      <div class="mx-4 hidden-sm-and-down"></div>
                    </v-card-actions>
                  </v-card>
                </v-hover>
              </v-col>
            </v-row>
          </v-item-group>
          </v-container>
      </v-sheet>
      </v-card>

</template>

<script>
import axios from 'axios'
import BottomNavigation from '@/components/BottomNavigation'

export default {
  data: () => ({
        reservations: [ ] ,
        companies: [ ],
        show: false,
        selected: [],
        expand: false,
        expand2: false,
        show: false,
        months: ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre'],
        days: ['Domingo', 'Lunes', 'Martes', 'Miércoles', 'Jueves', 'Viernes', 'Sábado',],
        activeBtn: 1,
        showNav: true,
        color: false
    }),
     components: {
    BottomNavigation
  },
    methods: {
      getCompanies() {
      const path = 'http://192.168.1.20:8000/sport/companies/'
      axios.get(path).then((response)=> {
        this.companies = response.data
        console.log(response.data);
        
      })
      }
    },
    created(){
      this.getCompanies()
    }
}
</script>

<style scoped>
  .v-card {
    transition: opacity .4s ease-in-out;
  }
  .v-card:not(.on-hover) {
    opacity: 0.9;
  }
  .show-btns {
    color: rgba(255, 255, 255, 1) !important;
  }
  .round{
        border-radius: 10px;
   }
  .container {
      max-width: 100%;
     max-height: 100%;

  }
   .description {
     position: absolute;
     margin-top: 3.5em;
     margin-left: 0.2em;
   }
   .item-icon {
     position: absolute;
     left: 0.5em;
     bottom: 0.5em;
   }
   .icon {
     position: absolute;
     left: 2.5em;
     bottom: 1.4em;
   }
    .item-icon2 {
     position: absolute;
     left: -0.5em;
     top: 0.5em;
   }
   .icon2 {
     position: absolute;
     left: 2.5em;
     bottom: -0.3em;
   }
   .bottom {
     margin-bottom: 50px;
   }
</style>
