<template>
  <v-app class="background">
    <v-container>
      <v-card class="mx-auto" max-width="344">
        <v-img :src="heroes.data.image.url" height="350px"></v-img>
        <v-card-subtitle class="text-center py-3">
          {{ heroes.data.biography["full-name"] }}
        </v-card-subtitle>
        <v-card-title class="justify-center pa-0 display-1 font-weight-bold red--text">
          {{ heroes.data.name }}
        </v-card-title>

        <v-card-actions>
          <v-btn color="red" text> BIO </v-btn>

          <v-spacer></v-spacer>

          <v-btn icon @click="show = !show">
            <v-icon>{{ show ? "mdi-chevron-up" : "mdi-chevron-down" }}</v-icon>
          </v-btn>
        </v-card-actions>

        <v-expand-transition>
          <div v-show="show">
            <v-divider></v-divider>

            <v-card-text class="ma-0 pa-0">
              <v-simple-table>
                <template v-slot:default>
                  <tbody>
                    <tr>
                      <td class="text-left font-weight-bold caption">
                        Alter Egos
                      </td>
                      <td class="text-left font-weight-regular caption">
                        {{heroes.data.biography['alter-egos']}}
                      </td>
                    </tr>
                    <tr>
                      <td class="text-left font-weight-bold caption">
                        Alignment
                      </td>
                      <td class="text-left font-weight-regular caption">
                        {{heroes.data.biography.alignment}}
                      </td>
                    </tr>
                    <tr>
                      <td class="text-left font-weight-bold caption">
                        Publisher
                      </td>
                      <td class="text-left font-weight-regular caption">
                        {{heroes.data.biography.publisher}}
                      </td>
                    </tr>
                    <tr>
                      <td class="text-left font-weight-bold caption">
                        First-appearance
                      </td>
                      <td class="text-left font-weight-regular caption">
                        {{heroes.data.biography['first-appearance']}}
                      </td>
                    </tr>
                    <tr>
                      <td class="text-left font-weight-bold caption">
                        Place of birth
                      </td>
                      <td class="text-left font-weight-regular caption">
                        {{heroes.data.biography['place-of-birth']}}
                      </td>
                    </tr>
                    <tr>
                      <td class="text-left font-weight-bold caption">
                        Aliases
                      </td>
                      <td class="text-left font-weight-regular caption" >
                        <p v-for="(alias, index) in aliases" :key="index">
                          {{alias}}
                        </p>
                      </td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-card-text>
          </div>
        </v-expand-transition>

        <v-card-actions class="red white--text">
          <v-card-title class=" "> Powerstats </v-card-title>

          <v-spacer></v-spacer>

          <v-btn icon @click="showStats = !showStats">
            <v-icon color="white">{{
              showStats ? "mdi-chevron-up" : "mdi-chevron-down"
            }}</v-icon>
          </v-btn>
        </v-card-actions>

        <v-expand-transition >
          <div v-show="showStats" class="red pa-0 white--text">
            <v-divider class="px-10 gray mb-5" />
            <v-row>
              <v-col cols="4">
                <v-card-title class="body-2 justify-center pa-1">
                  Combat
                </v-card-title>
                <p class="text-center">{{ heroes.data.powerstats.combat }}</p>
              </v-col>
              <v-col cols="4">
                <v-card-title class="body-2 justify-center pa-1">
                  Durability
                </v-card-title>
                <p class="text-center">{{ heroes.data.powerstats.durability }}</p>
              </v-col>
              <v-col cols="4">
                <v-card-title class="body-2 justify-center pa-1">
                  Intelligence
                </v-card-title>
                <p class="text-center">{{ heroes.data.powerstats.intelligence }}</p>
              </v-col>
              <v-col cols="4">
                <v-card-title class="body-2 justify-center pa-1">
                  Power
                </v-card-title>
                <p class="text-center">{{ heroes.data.powerstats.power }}</p>
              </v-col>
              <v-col cols="4">
                <v-card-title class="body-2 justify-center pa-1">
                  Speed
                </v-card-title>
                <p class="text-center">{{ heroes.data.powerstats.speed }}</p>
              </v-col>
              <v-col cols="4">
                <v-card-title class="body-2 justify-center pa-1">
                  Strength
                </v-card-title>
                <p class="text-center">{{ heroes.data.powerstats.strength }}</p>
              </v-col>
            </v-row>
          </div>
        </v-expand-transition>
      </v-card>
    </v-container>
  </v-app>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import axios from "axios";

export default {
  name: "Home",
  components: {},
  data() {
    return {
      show: false,
      heroes: "",
      showStats: false,
      aliases: '',
    };
  },
  methods: {
    async getHero() {
      try {
        let getRandomInt = (min, max) => {
          return Math.floor(Math.random() * (max - min)) + min;
        };
        let numRandom = getRandomInt(1, 732);
        let datos = await axios.get(
          `https://www.superheroapi.com/api.php/10224954304343507/${numRandom}`
        );
        this.heroes = datos;
        this.aliases = datos.data.biography.aliases;
        console.log(datos.data);
      } catch (error) {
        console.log(error);
      } finally {
        console.log("probando");
      }
    },
  },
  created() {
    this.getHero();
  },
};
</script>
<style lang="sass">

  .background
    background-image: url('../assets/imgs/background.png') !important
    background-size: cover !important
    background-repeat: no-repeat !important
    background-attachment: fixed !important
</style>
