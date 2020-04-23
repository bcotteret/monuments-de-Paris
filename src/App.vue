<template>
  <div id="app">
    <div class="row mb-1">
      <h1 class="container">Monuments de Paris</h1>
    </div>
    <div class="row">
      <div class="col-12 col-lg-8">
        <map-box :sites="sites"/>
      </div>
      <div class="col-12 col-lg-4">
        <b-list-group class="mt-3 mt-lg-0" v-for="site in sites" :key="site.id">
          <b-list-group-item  class="flex-column align-items-baseline">
            <div class="d-flex w-100 justify-content-between">
              <h5 class="mb-1">
                <strong>{{site.id}}</strong> {{site.name}}
              </h5>
              <div class="badge pill" :class="site.categorie">
                {{site.categorie}}
              </div>
            </div>
          </b-list-group-item>          
        </b-list-group>
      </div>  
    </div>
  </div>
</template>

<script>
import MapBox from './components/MapBox.vue';
import Sites from './sites.json';
import 'bootstrap/dist/css/bootstrap.css'
export default {
  name: 'App',
  components: {
    MapBox
  },
  data(){
    return{
      sites: Sites
    };
  }
}
</script>

<style>
#app {
  font-family: Helvetica, ubuntu, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
.pill {
  color: #fefefe;
  font-weight: bold;
}
.commemoratif {
  background: #c30b82;
}
.circulation {
  background: #4838cc;
}
.approvisionnement {
    background: #60d140;
}
.commerce {
  background: #f9a53e;
}

.hygiene {
  background: #9d4fad;
}

</style>
