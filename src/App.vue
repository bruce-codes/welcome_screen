<!-- AIzaSyAFeuHFnWgx5aJYG6LDcUEl-Pc5otF6YXE -->
<script>
  import Container from './components/Container.vue'
  import Card from './components/Card.vue'
  import Footer from './components/Footer.vue'

  export default {
    name: "App",
    components: {
      Container,
      Card,
      Footer
    },
    data() {
      return {
        title: "Welcome to Opportunity",
        sheet_id: import.meta.env.VITE_GOOGLE_SHEET_ID,
        api_token: import.meta.env.VITE_GOOGLE_API_KEY,
        entries: []
      };
    },
    
    computed: {
      gsheet_url() {
        return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
      },

      currentDate() {
        var date = new Date();
        return date.getDate() + "." + (date.getMonth() + 1) + "." + date.getFullYear();
      }
    },

  methods: {
    async getData() {
      const response = await fetch(this.gsheet_url);
      const data = await response.json();
      this.entries = data.valueRanges[0].values;
    }
},

mounted() {
    this.getData();
}
}

</script>

<template>   
  <Container>

    <div class="site-title">      
      <h1>
        {{ title }}
      </h1>
    </div> 

    <div class="date">
      <h1>{{ currentDate }}</h1>
    </div>


      <!-- DAS IST DIE CARD -->
      <Card v-for="entry in entries">
        <h2 class="h2red">
         {{ entry[0] }}, {{ entry[1] }}
        </h2>
        <p class="p" id="fett">
          {{ entry[2] }}
        </p>
        <p class="p">
          {{ entry[3] }}
        </p>
      </Card>

      <Footer/>

    </Container> 
</template>

<style>

body{
  background-color: #E8EFF4;
}
h1 {
  margin: 0px;
}

.site-title {
  margin-bottom: 0px;
  font-weight: 900;
  font-size: 35px;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}

.date {
  font-size: 38px;
  color: #9AA7B1;
  margin: 0;
  height: 50px;
}

.h2red {
  color: #EB5E00;
  font-size: 30px;
}

.p {
  color: #FFBFAB;
  font-size: 25px;
}
#fett {
  font-weight: bold;
}


</style>
