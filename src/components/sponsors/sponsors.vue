<template>
  <div id="sdtet-sponsors-section" class="sdtet-container">
    <div class="sdtet-divider"></div>
    <div class="ml-5 mr-5 mb-5">
      <v-layout row wrap>
        <v-flex xs12 md5 lg5>
          <h1 id="sponsors">Sponsors</h1>
          <p v-if="sponsorData.sponsorSignUp">
            <v-btn style="width:350px" v-bind:href="sponsorData.applicationURL" target="_blank" block round color="teal" dark>Download Sponsorship Application </v-btn>
          </p>
          <p>
            <b>Questions or details?: </b>
            <a href="mailto:sponsor@sdtet.com">sponsor@sdtet.com</a>
          </p>
          <div v-for="text in sponsorData.text" :key="text.id">
            <p>{{text}}</p>
          </div>
          <p>
            <ul v-for="text in sponsorData.benefitsList" :key="text.id">
              <li>{{text}}</li>
            </ul>
          </p>
          <div v-for="text in sponsorData.closingText" :key="text.id">
            <p>{{text}}</p>
          </div>
        </v-flex>

        <v-flex xs12 md7 lg7 class="sdtet-text-align-center">
          <h1 class="sdtet-h1-spacer">&nbsp;</h1>
          <h2>{{sponsorData.slogan}}</h2>
          <v-layout class="sdtet-sponsors-logos-container" row wrap justify-space-around>
            <a v-for="sponsor in sponsors"  :key="sponsor.id" :href="sponsor.url" target="_blank">
              <img class="ma-3" :src="sponsor.logo_image_link">
            </a>
          </v-layout>
        </v-flex>

      </v-layout>
    </div>
  </div>
</template>

<script type="text/javascript">
  import axios from 'axios'
  import data from './sponsors.json'

  export default {
    data () {
      return {
        sponsors: [],
        sponsorData: data
      }
    },
    created () {
      axios.get('https://cors-anywhere.herokuapp.com/http://admin.sdtet.com/php_file/get_sponsors.php')
        .then(response => {
          // JSON responses are automatically parsed.
          this.sponsors = response.data
          //console.log('Sponsors: ', response.data)
        })
        .catch(e => {
          console.log(e)
        })
    }
  }
</script>

<style lang="scss">
  @import 'sponsors';
</style>