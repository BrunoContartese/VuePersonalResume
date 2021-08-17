<template>
  <v-card
    color="grey lighten-4"
    light
  >
    <v-card-text>
      <content-section
        title="Who am I?"
      >
        I'm a backend developer, born in Argentina.
        I'm interested and skilled in different topics of Information Technology including programming, web development, computer and network security.
      </content-section>
      <content-section
        v-if="educations"
        title="Education"
      >
        <v-layout
          v-for="(education, i) in educations"
          :key="i"
        >
          <v-flex md4>
            {{ education.from }} - {{ education.to }}
          </v-flex>
          <v-flex md8>
            <strong v-if="education.title">{{ education.title }}</strong>
            <div v-if="education.location">
              <i>{{ education.location }}</i>
            </div>
            <div v-if="education.description">
              {{ education.description }}
            </div>
          </v-flex>
        </v-layout>
      </content-section>
      <content-section
        v-if="publications"
        title="Publications"
      >
        <v-layout
          v-for="(publication, i) in publications"
          :key="i"
        >
          <v-flex md4>
            {{ publication.date }}
          </v-flex>
          <v-flex md8>
            <strong v-if="publication.title">{{ publication.title }}</strong>
            <div v-if="publication.description">
              <span v-html="publication.description" />
            </div>
          </v-flex>
        </v-layout>
      </content-section>
      <content-section
        v-if="conferences"
        title="Conference attendance"
      >
        <v-layout
          v-for="(conference, i) in conferences"
          :key="i"
        >
          <v-flex md4>
            {{ conference.date }}
          </v-flex>
          <v-flex md8>
            <strong v-if="conference.title">{{ conference.title }}</strong>
          </v-flex>
        </v-layout>
      </content-section>
      <content-section
        v-if="skills"
        id="to-timeline"
        title="Skills"
      >
        <template slot="actions">
          (% are relative not absolute)
        </template>
        <v-layout wrap>
          <template
            v-for="(skill, i) in skills"
          >
            <v-flex
              v-if="skill.divider"
              :key="i"
              md12
              xs12
              mb-4
            />
            <v-flex
              v-else
              :key="i"
              md6
              xs12
            >
              <div
                class="mr-2 ml-2"
              >
                <div class="align-center">
                  <v-icon
                    small
                  >
                    {{ skill.icon }}
                  </v-icon>
                  {{ skill.title }}
                </div>
                <v-progress-linear
                  class="progress"
                  color="secondary"
                  height="3"
                  :value="skill.value"
                />
              </div>
            </v-flex>
          </template>
        </v-layout>
      </content-section>
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from '@/views/dark-template/content/Section'
export default {
  name      : 'MainContent',
  components: { ContentSection },
  data      : () => ({
    conferences: [
      {
        date : '2013',
        title: 'Argentine Conference on Embedded Systems.- UBA.',
      },
      {
        date : '2014',
        title: 'Argentine Conference on Embedded Systems.- UBA.',
      },
      {
        date : '2014',
        title: 'Congreso de la Sociedad Argentina de Bioingeniería. San Nicolás de los Arroyos.',
      },
      {
        date : '2015',
        title: 'Argentine Conference on Embedded Systems.- UBA.',
      },
      {
        date : '2016',
        title: 'Argentine Conference on Embedded Systems.- UBA. (as exponent)',
      },
    ],
    publications: [
      {
        date       : '2016',
        title      : 'ItamCare: Otoemisor Acústico y Potenciales Auditivos Evocados',
        description: '<a href="https://www.researchgate.net/publication/309721477_ItamCare_Otoemisor_Acustico_y_Potenciales_Auditivos_Evocados" target="_blank">Paper</a>',
      },
    ],
    educations: [
      {
        from       : '2009',
        to         : '2011',
        title      : 'High School degree in organizations and economics',
        location   : 'Ntra. Sra. de la Misericordia, San Nicolás de los Arroyos, Bs. As',
        description: 'Finished high school',
      },
      {
        from       : '2012',
        to         : '2021 (Not finished yet)',
        title      : 'Bachelor\'s degree, Electronics Engineering',
        location   : 'National Technological University, San Nicolás de los Arroyos, Bs. As',
        description: 'Became a member of National Technological University',
      },
      {
        from       : '2017',
        to         : '2017',
        title      : 'Industrial Automation',
        location   : 'National Technological University, Gral. Pacheco, Bs. As',
        description: 'Rapid language intensive course.',
      },
      {
        from       : '2017',
        to         : '2017',
        title      : 'Computer Forensics',
        location   : 'CESBA, Rosario, Santa Fe',
        description: 'Computer forensics teorical course.',
      },
    ],
    skills: [
      {
        title: 'PHP',
        icon : 'mdi-language-php',
        value: 100,
      },
      {
        title: 'JavaScript',
        icon : 'mdi-language-javascript',
        value: 100,
      },
      {
        title: 'Laravel Framework',
        icon : 'mdi-laravel',
        value: 100,
      },
      {
        title: 'Vue.js Framework',
        icon : 'mdi-vuejs',
        value: 90,
      },
      { divider: true },
      {
        title: 'Angular.js Framework',
        icon : 'mdi-angularjs',
        value: 50,
      },
      {
        title: 'C/C++',
        icon : 'mdi-language-cpp',
        value: 80,
      },
      {
        title: 'Qt Framework',
        icon : 'mdi-language-cpp',
        value: 40,
      },
      {
        title: 'Rapid (ABB Robotics)',
        icon : 'mdi-robot',
        value: 40,
      },
      { divider: true },
      {
        title: 'Ubuntu Server',
        icon : 'mdi-ubuntu',
        value: 90,
      },
      {
        title: 'CentOS Server',
        icon : 'mdi-linux',
        value: 60,
      },
      {
        title: 'Windows Server',
        icon : 'mdi-windows',
        value: 80,
      },
      {
        title: 'Git',
        icon : 'mdi-git',
        value: 100,
      },
      { divider: true },
      {
        title: 'Networking',
        icon : 'mdi-wan',
        value: 90,
      },
      {
        title: 'Networking - Microtik',
        icon : 'mdi-router-wireless',
        value: 70,
      },
      { divider: true },
      {
        title: 'Proxmox',
        icon : 'mdi-laptop',
        value: 70,
      },
      {
        title: 'Digital Ocean',
        icon : 'mdi-server',
        value: 100,
      },
      {
        title: 'AWS',
        icon : 'mdi-server',
        value: 50,
      },
      {
        title: 'Apache',
        icon : 'mdi-server',
        value: 100,
      },
      { divider: true },
      {
        title: 'Leadership',
        icon : 'mdi-account-group',
        value: 80,
      },
    ],
  }),
}
</script>

<style scoped>
.title {
  border-bottom: 2px #bfbfbf solid;
  line-height: 1.5 !important;
}
.progress {
  margin-top: 0.1rem;
}
</style>
