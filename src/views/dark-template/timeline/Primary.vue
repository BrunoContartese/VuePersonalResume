<template>
  <v-card
    color="grey lighten-4"
    light
  >
    <v-card-text>
      <content-section
        id="timeline"
        :title="detailed ? 'My Life in a Nutshell' : 'My Experiences'"
      >
        <template slot="actions">
          <div>
            <v-switch
              v-model="detailed"
              :label="detailed ? 'Detailed' : 'Summary'"
            />
          </div>
        </template>

        <v-timeline
          dense
        >
          <v-timeline-item
            v-for="(item, i) in orderedItems"
            :key="i"
            :icon="item.icon || ''"
            :class="{transparent: item.transparent}"
            large
          >
            <template
              v-if="item.iconImage"
              v-slot:icon
            >
              <v-avatar>
                <img
                  :src="publicPath(item.iconImage)"
                >
              </v-avatar>
            </template>
            <template v-slot:opposite />
            <v-layout>
              <v-flex
                v-if="$vuetify.breakpoint.smAndUp"
                md1
                sm2
                align-self-center
              >
                <span>{{ item.year }}</span>
              </v-flex>
              <v-flex
                md11
                sm10
                xs12
              >
                <v-card class="elevation-1">
                  <v-card-title class="pb-0">
                    <div>
                      <p v-if="$vuetify.breakpoint.xsOnly">
                        {{ item.year }}
                      </p>
                      <h3>{{ item.title }}</h3>
                    </div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout wrap>
                      <v-flex
                        :md7="!!item.image"
                        :md12="!item.image"
                        xs12
                      >
                        <div class="mr-1">
                          <span
                            v-if="item.text"
                            class="pre"
                          >{{ item.text }}</span>
                          <!-- eslint-disable vue/no-v-html -->
                          <div
                            v-else-if="item.html"
                            v-html="item.html"
                          />
                          <!-- eslint-enable vue/no-v-html -->
                        </div>
                      </v-flex>
                      <v-flex
                        v-if="item.image"
                        md5
                        xs12
                      >
                        <div
                          class="mt-2"
                        >
                          <v-carousel
                            v-if="Array.isArray(item.image)"
                            :show-arrows="false"
                            :height="325"
                          >
                            <v-carousel-item
                              v-for="(citem,ci) in item.image"
                              :key="ci"
                              :src="publicPath(citem)"
                            />
                          </v-carousel>
                          <v-img
                            v-else
                            :max-height="item.imageHeight ? item.imageHeight : ''"
                            :src="publicPath(item.image)"
                          />
                        </div>
                      </v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-timeline-item>
        </v-timeline>
      </content-section>
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from '@/views/dark-template/content/Section'
export default {
  name      : 'Timeline',
  components: { ContentSection },
  data      : () => ({
    detailed: false,
    items   : [
      {
        year : '2015-2017',
        title: 'Software developer',
        html : `<b><a href="https://www.frsn.utn.edu.ar/frsn/" target="_blank">National Technological University</a></b><br>
                    This was my first non freelancer job. It was a part-time trainee position in a research laboratory at the university.<br>
                    i've worked in the development of an acoustic otoemitter and auditory evoked potentials (Detection of hearing loss in neonates).<br>
                    Some of tasks that i did:
                    <ul>
                      <li>Compilation of a custom operating system based on GNU / Linux using BUILDROOT. (We made a 64MB kernel) </li>
                      <li>Software development using <a href="https://qt.io/" target="_blank">QT Framework</a> and compiling for ARM architecture.</li>
                    </ul>
                  `,
        icon: 'mdi-office-building',
      },
      {
        year : '2017-2021',
        title: 'IT department head',
        html : `<b><a href="https://fnsr.com.ar/" target="_blank">Fundación Nuestra Señora del Rosario Hospital</a></b><br>
                    In this job i was responsable of it and processes department<br>
                    This hospital has more than 210 computers, 255 internation patient beds and last generation imagenology equipment. <br>
                    Some of tasks that i did:
                    <ul>
                      <li>Design and implementation of wired network</li>
                      <li>Software development</li>
                      <li>Technical assistance for Siemens, Philips and Sonoscape equipment. (Tomographs, Resonator, Ultrasounds, etc)</li>
                      <li>Process design and analysis</li>
                      <li>Team leader</li>
                      <li>Technical and academic support for decision-making of several sectors. (Management, Accounting, Billing office, Test Laboratory, among others)</li>
                    </ul>
                  `,
        icon: 'mdi-hospital-building',
      },
      {
        year : 'Present',
        title: 'Backend developer',
        html : `<b><a href="https://estoes.me/" target="_blank">Esto es Agency</a></b><br>
                    In the present, i'm working as Sr. Backend developer at Esto Es Agency.<br>
                    Some of tasks that i do:
                    <ul>
                      <li>Software Architecture Design and implementation</li>
                      <li>Software Develop using <a href="https://laravel.com/" target="_blank">Laravel framework</a> (Php)</li>
                      <li>Software Develop using <a href="https://adonisjs.com//" target="_blank">Adonis framework</a> (Node.js)</li>
                    </ul>
                  `,
        icon: 'mdi-laptop',
      },
    ],
  }),
  computed: {
    orderedItems () {
      const items = [...this.items].reverse()
      if (this.detailed)
        return items
      return items.filter((item) => {
        return !item.detailed
      })
    },
  },
}
</script>

<style scoped>
.title {
  border-bottom: 2px #bfbfbf solid;
  line-height: 1.5 !important;
}
.pre {
  white-space: pre;
}
.transparent{
  opacity: 0.6;
}
</style>
