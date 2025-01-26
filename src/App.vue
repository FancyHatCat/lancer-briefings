<template>
  <Header :header="this.header" />
  <div class="content-container">
    <section class="section-container" id="missions" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/mission-icon.svg" />
        <h1>Logs</h1>
      </div>
      <div class="section-content-container">
        <h3>Current Assignment</h3>
        <Markdown :source="current_md" class="markdown" />
        <h3>Mission List</h3>
        <div class="mission-list-container">
          <Mission
            v-for="item in this.missions"
            :key="item.slug"
            :mission="item"
            :selected="this.mission_slug"
            @click="selectMission(item)"
          />
        </div>
      </div>
    </section>
    <section class="section-container" id="events" style="width:435px; height:714px;">
      <div class="section-header clipped-medium-backward">
        <img src="/icons/events-icon.svg" />
        <h1>Briefing</h1>
      </div>
      <div class="section-content-container">
        <Markdown :source="events" class="markdown" />
      </div>
    </section>
    <section class="section-container" id="pilots" style="width:894px; height:714px;">
      <div style="height:52px; overflow:hidden;">
        <div class="section-header clipped-medium-backward-pilot">
          <img src="/icons/pilot-icon.svg" />
          <h1>Roster</h1>
        </div>
        <div class="rhombus-back">&nbsp;</div>
      </div>
      <div class="section-content-container">
        <div class="pilot-list-container">
          <Pilot v-for="item in this.pilots" :key="item.slug" :pilot="item" />
        </div>
      </div>
    </section>
  </div>
  <svg
    style="visibility: hidden; position: absolute;"
    width="0"
    height="0"
    xmlns="http://www.w3.org/2000/svg"
    version="1.1"
  >
    <defs>
      <filter id="round">
        <feGaussianBlur in="SourceGraphic" stdDeviation="5" result="blur" />
        <feColorMatrix
          in="blur"
          mode="matrix"
          values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -5"
          result="goo"
        />
        <feComposite in="SourceGraphic" in2="goo" operator="atop" />
      </filter>
    </defs>
  </svg>
  <audio autoplay>
    <source src="/startup.ogg" type="audio/ogg" />
  </audio>
  <Footer/>
</template>

<script>
import Header from './components/layout/Header.vue';
import Footer from './components/layout/Footer.vue';
import Mission from './components/Mission.vue';
import Pilot from './components/Pilot.vue';
import Markdown from 'vue3-markdown-it';

export default {
  components: {
    Header,
    Footer,
    Mission,
    Pilot,
    Markdown
  },

  data() {
    return {
      "mission_slug": "003-A",
      "current_md": "",
      "events": "",
      "missions": [
        {
          "slug": "003-A",
          "name": "Space Invaders",
          "status": "start"
        },
        {
          "slug": "003-B",
          "name": "Raiders of the Lost Cargo",
          "status": "start"
        },
        {
          "slug": "002-A",
          "name": "Under a Mausoleum's Shadow",
          "status": "success"
        },
        {
          "slug": "002-B",
          "name": "Graveyard Shift",
          "status": "success"
        },
        {
          "slug": "001-A",
          "name": "Asteroids (Sector 1)",
          "status": "success"
        },
        {
          "slug": "001-B",
          "name": "Asteroids (Sector 2)",
          "status": "partial-success"
        },
      ],
      "pilots": [
        {
          "callsign": "Alceste",
          "alias": "Cécile Zhen",
          "code": "nUO9sckU-wrVY-eCQw-KTSL-Cw9tCGogR3TB///VggL-ke6S-NXnaTO4a-ENMxnbnI//lxAgxlgv-GUgv-10GV-rsIn-qqZnOmnbAuJ5",
          "corpro": "SSC",
          "frame": "Swallowtail",
          "mech": "Strega",
          "status": "ACTIVE"
        },
        {
          "callsign": "Azure",
          "alias": "Roy Spencer",
          "code": "kprMs5AI-W4lN-hzRc-JH0y-QUv4peyYoXsk///WU6h-QfH9-DrpaUNYa-HDkwq2VY//nmjhYuKy-U7qL-XL0T-DgWV-ZPvvpbWSEGEN",
          "corpro": "IPS-N",
          "frame": "Rayleigh",
          "mech": "Skies Unknown",
          "status": "ACTIVE"
        },
        {
          "callsign": "Jackal",
          "alias": "Layla Nour",
          "code": "DTLYykhs-E9YW-KH14-f7Ym-TQFufKKSt7QA///CapS-kzZE-EgrwVq4G-ZybLIQnr//mWS2hEmC-f3By-5SZN-LYcm-jaK8HFVNda7D",
          "corpro": "HA",
          "frame": "Barbarossa",
          "mech": "Anubis",
          "status": "ACTIVE"
        },
        {
          "callsign": "Lazarus",
          "alias": "Helios Nonagessimus",
          "code": "5jogwSIq-BFNI-VK7U-xxIh-NnMVUPUe8gLv///BoN5-Wtb2-iT9x2UhG-RDGAdNSj//GK7nQCVy-pcZk-E0qZ-KUde-J6gaQF5ZKTh8",
          "corpro": "HA",
          "frame": "Sherman",
          "mech": "Nona",
          "status": "ACTIVE"
        },
        {
          "callsign": "Lysis",
          "alias": 'Erien Vachs',
          "code": "97JrvuAw-f524-r8Sd-mSs5-rOIJUD8x6Ai1///RFDC-MQnD-2qF36c0V-ZGnGuuip//Nxj2m4N1-hBac-dWfT-Q4Er-98FqLBMfjHOK",
          "corpro": "HA",
          "frame": "Sherman",
          "mech": "Hyperthermic Prognosis",
          "status": "ACTIVE"
        },
        {
          "callsign": "Mayhem",
          "alias": 'Rebecca "Bex"',
          "code": "tB4c0t0u-Nd64-7sht-nga4-H4pxQf74PEvy///fxlw-izW1-veXuSqz5-CxNWiJOh//6p6KgMmz-ccCc-gBsg-YeJ0-cSgAafUl4NOa",
          "corpro": "SSC",
          "frame": "Viceroy",
          "mech": "Gnaw Rabbit",
          "status": "ACTIVE"
        },
        {
          "callsign": "Mercury",
          "alias": 'Kaelyn Forsythe',
          "code": "JSb1e8Gy-QY9T-aetD-1vbt-6l3cmS5Kh56Q///VP4l-zzav-9NGTVynv-5X4EEUPH//ePlSWBv4-HxIl-TcFI-0eEm-7WW9SaJatKqE",
          "corpro": "SSC",
          "frame": "Atlas",
          "mech": "Swordmaster",
          "status": "ACTIVE"
        },
        {
          "callsign": "Sequence",
          "alias": 'Qasem Nurani',
          "code": "AeQSR29R-dZaD-xfxT-9n8g-UE0W4vDN2h1M///WxV0-xJeH-Hew0oTiJ-zJGPzSuf//F78NcGee-lzZB-ayOd-c4HA-H9C1o7JHDwTX",
          "corpro": "HA",
          "frame": "Sunzi",
          "mech": "Pahlevan",
          "status": "ACTIVE"
        },
      ],
      "header": {
        "planet": "ASTEROID MINING BASE",
        "year": "5101u",
        "system": "Tarf",
        "gate": "Ngoc Linh",
        "ring": "Annamite-Line [Ring 11]",
        "headerTitle": "Iron Orchids",
        "headerSubtitle": "Tactical Assets",
        "subheaderTitle": "Thalin Estel ",
        "subheaderSubtitle": "Private Network",
      },
      "options":{
        "eventsMarkdownPerMission": true
      }
    }
  },

  created() {
    this.loadMissionMarkdown()
    this.loadEventsMarkdown()
  },

  computed: {

  },

  methods: {
    selectMission(mission) {
      this.mission_slug = mission.slug;
      this.loadMissionMarkdown()
      if(this.options.eventsMarkdownPerMission){
        this.loadEventsMarkdown();
      }
    },
    loadMissionMarkdown() {
      let self = this;
      let md = `/missions/${self.mission_slug}.md`
      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.current_md = client.responseText;
      }
      client.send();
    },
    loadEventsMarkdown() {
      let self = this;
      let md = "";

      if(self.options.eventsMarkdownPerMission){
        md = `/events/${self.mission_slug}.md`
      }
      else {
        md = "/events.md"
      }

      var client = new XMLHttpRequest();
      client.open('GET', md);
      client.onreadystatechange = function () {
        self.events = client.responseText;
      }
      client.send();
    }
  }

}
</script>


<style lang="scss">
#app {
  width: 1902px;
  height: 1300px;
  overflow: hidden;
}
</style>
