<template>
  <v-card
    class="mx-auto"
    max-width="400"
    elevation="10"
  >
    <v-img
      class="white--text align-end"
      height="200px"
      :src="image"
    >
      <v-card-title>{{ name }}</v-card-title>
    </v-img>

    <v-card-subtitle class="pb-0">Semester {{ semester }}</v-card-subtitle>

    <v-card-text class="text--primary">
      <div>{{ teacher }}</div>
      <div class="blue-grey--text text--lighten-2" v-if="course">{{ course }}</div>
    </v-card-text>

    <v-card-actions>
        <v-btn text color="red" :href="course ? course : '#'" :disabled="!course">
            Go to course
            <v-icon>mdi-double_arrow</v-icon>
        </v-btn>
        <v-spacer></v-spacer>
        <v-tooltip bottom>
            <template v-slot:activator="{ on }">
                <v-btn v-if="toledo" v-on="on" text icon color="red" :href="toledo">
                    <v-icon>mdi-school</v-icon>
                </v-btn>
            </template>
            <span>Toledo</span>
        </v-tooltip>
        <v-tooltip bottom>
            <template v-slot:activator="{ on }">
                <v-btn v-if="ects" v-on="on" text icon color="red" :href="ects">
                    <v-icon>mdi-information</v-icon>
                </v-btn>
            </template>
            <span>ECTS</span>
        </v-tooltip>
        <v-tooltip bottom>
            <template v-slot:activator="{ on }">
                <v-btn v-if="slack" v-on="on" text icon color="red" :href="slack">
                    <v-icon>mdi-slack</v-icon>
                </v-btn>
            </template>
            <span>Slack</span>
        </v-tooltip>
        <v-tooltip bottom>
            <template v-slot:activator="{ on }">
                <v-btn v-if="github" v-on="on" text icon color="red" :href="github">
                    <v-icon>mdi-github-circle</v-icon>
                </v-btn>
            </template>
            <span>GitHub</span>
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
                    image: imagePlaceholder
                },
            }),
        }
    },
    computed: {
        name: function() {
            return this.page.frontmatter.name; 
        },
        course: function() {
            return this.page.frontmatter.course;
        },
        teacher: function() {
            return this.page.frontmatter.teacher;
        },
        semester: function() {
            return this.page.frontmatter.semester;
        },
        toledo: function() {
            return this.page.frontmatter.toledo;
        },
        ects: function() {
            return this.page.frontmatter.ects;
        },
        github: function () {
            return this.page.frontmatter.github;
        },
        slack: function () {
            return this.page.frontmatter.slack;
        },
        image: function() {
            let image_url = this.page.frontmatter.image;
            if(image_url === undefined) {
                return imagePlaceholder;
            }
            image_url = `~${this.page.path}${image_url}`; // TODO: This is not yet supported by vuepress...
            return image_url;
        }
    }
}
</script>