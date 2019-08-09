

<template>
<!--  eslint-disable  -->
  <!-- <div class="hello">
    <div v-for="font in fonts.items">
      <div>
        {{ font.family }}
      </div>
    </div>
  </div> -->

 <div v-if="allFonts" class="md-layout">
<font-picker :api-key="'AIzaSyC4xQCYKx3yedrK_ANpQl_4h1HZFv_jwe4'" :options="{}" :active-font="fontFamily" @change="myFunc"></font-picker>

<p class="apply-font" >TEST TEST TEST TESTTEST TESTTEST TEST</p>
    <!-- <md-card :key="id"  v-for="( font, id) in allFonts" class="md-layout-item md-primary">
      <md-card-header>
        <md-card-header-text>
          <div :style="`font-family: ${font.family}`" class="md-title">{{font.family}}</div>
          <div :style="`font-family: ${font.family}`" class="md-subhead ">TEST TEXT </div>
        </md-card-header-text>

        <md-card-media>
        </md-card-media>
      </md-card-header>

      <md-card-actions>
        <md-button>Action</md-button>
        <md-button>Action</md-button>
      </md-card-actions>
    </md-card> -->

  </div>

</template>

<script src="https://cdn.jsdelivr.net/npm/vue-resource@1.3.4"></script>
<script>
/* eslint-disable */
import FontPicker from 'font-picker-vue';

export default {
  name: "Fonts",
  props: {
    msg: String
  },
  components: {
    'font-picker': FontPicker
  },
  data() {
    return {
      allFonts: [],
      groupedFonts: [],
      fontFamily: 'Roboto'
    }
  },
  computed: {
    fonts() {
   if (this.allFonts) {
      for (const key in this.allFonts) {
        console.log(key);
        if (this.allFonts.hasOwnProperty(key)) {
          const element = this.allFonts[key];
          // this.groupedFonts[key][element.category] = element
        }
      }

        return this.allFonts.slice(0,10)
      }
      return {}
    }
  },
  methods: {
    myFunc($event) {
      console.log($event.family);

      this.fontFamily = $event.family


    }
  },
  mounted() {

    this.$http
      .get(
        "https://www.googleapis.com/webfonts/v1/webfonts?sort=popularity&key=AIzaSyC4xQCYKx3yedrK_ANpQl_4h1HZFv_jwe4"
      )
      .then(
        response => {
          // get body data
          this.allFonts = response.data.items;

          for (const key in this.allFonts) {
            if (this.allFonts.hasOwnProperty(key)) {
              const element = this.allFonts[key];
              this.allFonts[key].sort = "popularity"

            }
          }
          console.log(response);


        },
        response => {
          // error callback
        }
      );
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
