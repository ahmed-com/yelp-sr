<template>
  <v-app 
    ref="app"
  >

    <v-app-bar
      app
      clipped-right
      clipped-left
      :height="headerHeight"
      :color="isMobileDevice ? '#d32323' : 'grey lighten-5'"
    >
    <v-app-bar-nav-icon   @click="drawer = !drawer"></v-app-bar-nav-icon>
      <YelpSearch
        v-if="!isMobileDevice"
        class="search-input"
        servicePlaceholder="service"
        serviceTypeahead="Restaurant"
        :serviceSuggestions="serviceSuggestions"
      />

      <YelpSearchMobile
        v-if="isMobileDevice"
        class="search-input"
        id="mobile-search-input"
        servicePlaceholder="service"
        serviceTypeahead="Restaurant"
        :serviceSuggestions="serviceSuggestions"
      />
    </v-app-bar>

    <v-navigation-drawer
      v-model="drawer"
      :absolute="isFooterUp"
      :height="drawerHeight"
      app
      width="300"
      clipped      
      :style="{top: leftDrawerTop}"
      class="left-drawer grey lighten-5"
    >

      <!-- <v-list
        class="pl-14"
        shaped
      >
        <v-list-item
          v-for="n in 4"
          :key="n"
        > -->
          <!-- <v-list-item-content>
            <v-list-item-title>Filter {{ n }}</v-list-item-title>
          </v-list-item-content> -->
          <template v-for="m in 4" >
            <v-list subheader flat class="pl-14" :key="m" dense>
              <v-subheader>Group Filters {{m}}</v-subheader>
              <v-list-item-group>
                <v-list-item v-for="n in 4" class="filter-item" :key="`${m}${n}`" >
                  <v-checkbox color="grey"  :label="`Filter${n}`"> x</v-checkbox>
                </v-list-item>
              </v-list-item-group>
            </v-list>
          </template>
        <!-- </v-list-item>
      </v-list> -->
    </v-navigation-drawer>

    <v-navigation-drawer
      app
      v-model="showMap"
      clipped
      right
      fixed
      width="400"
      class="right-drawer"
    >
      <iframe
        width="100%"
        height="90%"
        style="border:0"
        loading="lazy"
        allowfullscreen
        src="https://www.google.com/maps/embed/v1/place?key=AIzaSyC0cZ8qI1PD_qwMAO7v8N31GjWQ8pCac84&q=Space+Needle,Seattle+WA">
      </iframe>
    </v-navigation-drawer>

    <v-main
     ref="main"
     class="grey lighten-5"
     >
      <v-container >
        <h1 class="header-text">Lorem ipsum dolor sit amet consectetur adipisicing :</h1>
        <v-row>
          <v-col
            v-for="n in 10"
            :key="n"
            cols="12"
          >
            <v-card
              class="mx-auto my-12"
              @mouseenter="changeElevation(n,false)"
              @mouseleave="changeElevation(n,true)"
              :flat="cardsElevation[n - 1]"
            >
              <v-row>
                <v-col cols="5">
                  <v-img
                    src="https://cdn.vuetifyjs.com/images/cards/cooking.png"
                    class="card-img ml-3"
                  ></v-img>
                </v-col>

                <v-col cols="7">

                  <v-card-title>Cafe Badilico</v-card-title>

                  <v-card-text>
                    <v-row
                      align="center"
                      class="mx-0"
                    >
                      <v-rating
                        :value="4.5"
                        color="amber"
                        dense
                        half-increments
                        readonly
                        size="14"
                      ></v-rating>

                      <div class="grey--text ms-4">
                        4.5 (413)
                      </div>
                    </v-row>

                    <div class="my-4 text-subtitle-1">
                      $ • Italian, Cafe
                    </div>

                    <div>Small plates, salads & sandwiches - an intimate setting with 12 indoor seats plus patio seating.</div>
                  </v-card-text>
                </v-col>
              </v-row>

            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <v-footer
      ref="footer"
      app
      color="grey lighten-2"
      absolute
      :class="showMap ? 'footer-desktop' : 'footer-mobile'"
    >
    Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quasi, laudantium neque eos minus, pariatur sint nostrum culpa ipsam, distinctio sit repudiandae vitae. Maxime suscipit similique dolorem eligendi eveniet perferendis, placeat, ab rerum non aliquam dolore corporis autem? Incidunt libero vitae sit, adipisci porro saepe culpa, omnis consectetur ad, quidem at aspernatur? Accusantium, ipsum! Ea accusamus minus eaque. Autem quis expedita veniam nesciunt doloribus eos in aliquid error sit reiciendis! Nostrum consequatur molestiae eius delectus deleniti blanditiis a non cum tempora ullam. Dolor veniam repellendus quaerat magni cupiditate eveniet officia nam unde, quam voluptas soluta quod minima reprehenderit a est accusantium. Eos enim, iusto non assumenda dolores aut delectus suscipit distinctio optio id deleniti natus, odit culpa beatae perferendis vero nulla placeat corrupti sequi aliquid voluptas consectetur est exercitationem molestiae. Porro quas officiis obcaecati, rerum error provident voluptate voluptatem perspiciatis ea. Numquam impedit repellat facilis quos rerum earum fugit nihil, aperiam eos, a, mollitia voluptatum reiciendis. Minima repellendus accusantium velit vitae dolor deserunt, quisquam soluta aliquid suscipit hic quasi, dicta eveniet autem reiciendis iusto animi aperiam exercitationem reprehenderit, quos delectus fugit perspiciatis tempora. Doloremque quisquam itaque sed? Optio, a saepe ab at veniam dignissimos ipsum explicabo, corporis atque provident commodi praesentium odit reiciendis fugit expedita ex vitae libero excepturi esse debitis, ullam repellat. Aliquid voluptate totam ipsa nulla amet vitae, adipisci et expedita dignissimos, dicta sunt suscipit! Natus iusto temporibus pariatur iure eos explicabo provident voluptates laudantium incidunt quam voluptatem enim, sed dolorem voluptatibus eaque sequi, optio cupiditate! Quae consectetur at voluptate aspernatur ducimus enim dignissimos vero architecto, ad vitae sed quis, ea quisquam optio eligendi non animi sunt quaerat, autem nulla earum rerum! Molestias id at laudantium mollitia non ipsam doloremque, voluptates explicabo error perspiciatis quia deleniti veniam voluptate repudiandae iure consequatur? Illum sit dolore voluptas dolor quasi, libero saepe fugiat modi hic quis animi, dignissimos soluta repellendus explicabo vel beatae aliquid voluptatem fugit nihil quia? Quasi alias deleniti repellat iure optio ea sint. Natus molestiae reprehenderit nisi aliquid hic ex corporis, culpa, fuga asperiores, cumque maxime ea voluptate voluptas minus laudantium est nemo excepturi neque vero? Recusandae optio, quam, eveniet fuga delectus deserunt laborum excepturi sunt nam aperiam impedit explicabo reiciendis fugiat distinctio cumque, a incidunt deleniti repudiandae eaque minima asperiores quia? Dolorum est rem consequatur placeat. Ipsum natus iure error quidem! At facere error sit aliquid. Nobis libero, nisi exercitationem molestias obcaecati minima error voluptatum id, dolor possimus porro vitae dolore numquam fugit nam odio! Voluptatibus in doloribus fugiat quam dolores odit nam tempore eveniet deleniti mollitia nostrum temporibus iusto, maxime, vitae modi nobis reprehenderit dolor molestiae aliquam corporis quibusdam culpa? Accusamus neque beatae ipsum qui, natus quas assumenda veritatis quasi, labore dignissimos velit architecto, eos saepe rerum. Distinctio perferendis possimus maxime quia illum praesentium nobis ipsa, voluptatibus rerum veniam facilis dignissimos. Quae dolor praesentium qui exercitationem molestias natus accusamus ullam error aliquid fuga porro eum voluptatem facere, architecto suscipit. Suscipit dignissimos laudantium perspiciatis laborum corporis dolor ratione, soluta aliquam recusandae nulla ut illo quibusdam unde aspernatur at?
    </v-footer>
  </v-app>
</template>

<script>
import YelpSearch from './components/YelpSearch'
import YelpSearchMobile from './components/YelpSearchMobile'

export default {
  name: 'App',

  components: {
    YelpSearch,
    YelpSearchMobile
  },

  data: function(){
    return{
      drawer: false,
      showMap: null,
      isFooterUp: false,
      scrollTop: 0,
      headerHeight: 100,
      leftDrawerTop: `${100}px`,
      serviceSuggestions: [
        "restaurants",
        "plumbers",
        "bla bla bla",
        "A",
        "B",
        "C",
        "D",
        "E",
        "F",
        "G",
        "H",
        "I",
        "J",
        "K",
      ],
      cardsElevation : [true, true, true, true, true, true, true, true, true, true]
    }
  },

  computed:{
    drawerHeight(){
      return `calc(100vh - ${this.headerHeight}px)`;
      // return `100vh`
    },

    isMobileDevice(){
      switch (this.$vuetify.breakpoint.name) {
          case 'xs': return true
          case 'sm': return true
          default : return false
        }
    }
  },

  methods:{
    init(){
      console.log('init')
      if(!this.isMobileDevice){
        console.log('false')
        this.$set(this, "drawer", true)
      }
    },

    getIsFooterUp(){
      if(!this.$refs.footer) return false;
      const rect = this.$refs.footer.$el.getBoundingClientRect();
      return rect.top <= (window.innerHeight || document.documentElement.clientHeight)
    },

    getScrollTop(){
      // if(!this.$refs.app) return 0;
      // return this.$refs.app.$el.scrollTop;

      const root = document.querySelector('html');
      return root.scrollTop;
    },

    handleDocumentScroll(){
      this.isFooterUp = this.getIsFooterUp();
      this.scrollTop = this.getScrollTop();
    },

    changeElevation(n,elevation){
      // this.cardsElevation[n - 1] = elevation;
      this.$set(this.cardsElevation, n - 1, elevation);
    }
  },

  watch: {
    isFooterUp(isIt){
      if(isIt) {
        this.leftDrawerTop = `${this.headerHeight + this.scrollTop}px`
      } else{
        this.leftDrawerTop = `${this.headerHeight}px`
      }
    }
  },

  mounted(){
    document.addEventListener('scroll',this.handleDocumentScroll);
    this.init();
  }
};
</script>

<style scoped>
.footer-desktop{
  padding: 60px 440px 60px 40px;
}

.footer-mobile{
  padding: 60px 40px;
}

.header-text{
  font-family: 'Poppins','Helvetica Neue',Helvetica,Arial,sans-serif;
  font-weight: 700;
  /* word-break: break-word !important;
  overflow-wrap: break-word !important;
   */
  color: rgba(43,39,60,1);
  line-height: 32px;
  font-size: 24px;
  letter-spacing: -0.4px;
  padding: 20px 10px 40px;
}

.search-input{
  width: 700px;
}

#mobile-search-input{
  margin: auto;
}

.left-drawer{
  max-height: unset !important;
  z-index: 3 !important;
}

.right-drawer{
  max-height: unset !important;
  /* height: 100% !important; */
}

.card-img{
  border-radius: 3px;
}

.filter-item{
  max-height: 0;
}

</style>