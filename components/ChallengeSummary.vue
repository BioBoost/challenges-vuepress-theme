<template>

        <v-card hover
          max-width="400"
        >
          <v-img
            class="white--text align-end"
            height="200px"
            :src="image"
          >
            <v-card-title>{{ name }}</v-card-title>
          </v-img>
                
          <v-card-media
            src="https://raw.githubusercontent.com/ijklim/simon-game/gh-pages/assets/img/bg--game-pad.jpg"
            height="150px"
          >
          </v-card-media>
          
          <v-card-text class="text--primary">
            <div>{{ description }}</div>
          </v-card-text>
          
          <v-card-actions>
            <v-chip>
              <v-icon left color="red">mdi-account</v-icon>
              {{ difficulty }}
            </v-chip>
            <v-spacer></v-spacer>
            <v-icon color=green v-if="hasUnitTests">mdi-test-tube</v-icon>
            <v-icon color=red v-if="!hasUnitTests">mdi-test-tube-off</v-icon>
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
                    image: imagePlaceholder
                },
            }),
        }
    },
    computed: {
        chapter: function() {
            return this.page.frontmatter.chapter; 
        },
        name: function() {
            return this.page.frontmatter.name;
        },
        description: function() {
            return this.page.frontmatter.description;
        },
        difficulty: function() {
            return this.page.frontmatter.difficulty;
        },
        keywords: function() {
            return this.page.frontmatter.keywords;
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
        }
    }
}
</script>

<style scoped>
.border {
    border-radius:50px;
}
</style>