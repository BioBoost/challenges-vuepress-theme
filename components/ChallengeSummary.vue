<template>
  <v-card hover>
    <div v-if="isSolved" class="ribbon ribbon-top-right rbGreen"><span>Solved !</span></div>

    <v-card-title class="grey darken-3 white--text">{{ name }}</v-card-title>
    
    <v-img height="100px" :src="image" />
    
    <v-card-text class="text--primary">
      <div>{{ description }}</div>
    </v-card-text>
    
    <v-card-actions>

      <v-container fluid>
        <v-chip v-for="keyword in keywords" class="ml-1">{{ keyword }}</v-chip>
      </v-container>

      <v-spacer></v-spacer>

      <v-tooltip top v-if="notes">
        <template v-slot:activator="{ on }">
          <v-icon color="orange" v-on="on">mdi-message-text</v-icon>
        </template>
        <span>{{ notes }}</span>
      </v-tooltip>

      <v-tooltip right v-if="hasUnitTests">
        <template v-slot:activator="{ on }">
          <v-icon color="green" v-on="on">mdi-test-tube</v-icon>
        </template>
        <span>With Unit Tests</span>
      </v-tooltip>

      <v-tooltip right v-if="!hasUnitTests">
        <template v-slot:activator="{ on }">
          <v-icon color="red" v-on="on">mdi-test-tube-off</v-icon>
        </template>
        <span>Without Unit Tests</span>
      </v-tooltip>

    </v-card-actions>
  </v-card>
</template>

<script>
const imagePlaceholder = 'https://cdn.vuetifyjs.com/images/cards/docks.jpg';
export default {
  props: {
    page: {
      type: Object,
      default: () => ({
        frontmatter: {
          image: imagePlaceholder,
        },
      }),
    }
  },
  computed: {
    name: function() {
      return this.page.frontmatter.name;
    },
    description: function() {
      return this.page.frontmatter.description;
    },
    difficulty: function() {
      return this.page.frontmatter.difficulty;
    },
    difficultyColor: function() {
      return {
        'easy': 'green',
        'medium': 'orange',
        'hard': 'red',
      }[this.difficulty()];
    },
    keywords: function() {
      const frontmatterKeywords = this.page.frontmatter.keywords;
      if (frontmatterKeywords) return frontmatterKeywords.split(',').map((k) => k.trim());
      else return [];
    },
    image: function() {
      let image_url = this.page.frontmatter.image;
      if(image_url === undefined) {
        return imagePlaceholder;
      }
      image_url = `~${this.page.path}${image_url}`; // TODO: This is not yet supported by vuepress...
      return image_url;
    },
    hasUnitTests: function() {
      return this.page.frontmatter.unitTests;
    },
    isSolved: function() {
      return this.page.frontmatter.solved;
    },
    notes: function() {
      return this.page.frontmatter.notes;
    }
  }
}
</script>

<style scoped>
/* Source of Ribbon: https://codepen.io/nxworld/pen/oLdoWb */
@import url(https://fonts.googleapis.com/css?family=Lato:700);

.ribbon {
  width: 100px;
  height: 100px;
  overflow: hidden;
  position: absolute;
  z-index: 50;
  border-radius: 0 !important;
}

.ribbon::before,
.ribbon::after {
  position: absolute;
  z-index: -1;
  content: '';
  display: block;
  border-width: 5px;
  border-style: solid;
}

.ribbon span {
  position: absolute;
  display: block;
  width: 195px;
  padding: 6px 0;
  color: white;
  font: 700 12px/1 'Lato', sans-serif;
  text-shadow: 0 1px 1px rgba(0,0,0,.2);
  text-transform: uppercase;
  text-align: center;
}

.ribbon-top-right {
  top: -10px;
  right: -10px;
}
.ribbon-top-right::before,
.ribbon-top-right::after {
  border-top-color: transparent;
  border-right-color: transparent;
}
.ribbon-top-right::before {
  top: 0;
  left: 0;
}
.ribbon-top-right::after {
  bottom: 0;
  right: 0;
}
.ribbon-top-right span {
  left: -40px;
  top: 30px;
  transform: rotate(45deg);
}

.ribbon.rbGreen > span {
  background-color: #4caf50;
}

.ribbon.rbGreen::before,
.ribbon.rbGreen::after {
  border-color:  #4caf50;
  border-radius: 0;
}
</style>