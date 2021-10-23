<template>
    <div 
        class="container" 
        ref="container"
    >
        <span 
            class="typeahead" 
            id="service-typeahead" 
            :class="isComponentFocused ? '' : 'unfocused-service'"
        >{{computedServiceTypeahead}}</span>
        <input 
            type="text"
            @focus="isServiceFocused = true"
            @blur="isServiceFocused = false"
            autocomplete="off"
            id="service-input"
            class="input"
            :class="isComponentFocused ? '' : 'unfocused-service'"
            :placeholder="servicePlaceholder"
            v-model="service"
        >
        <div v-show="isComponentFocused" id="line-break"></div> 
        <span 
            v-show="isComponentFocused"
            class="typeahead" 
            id="location-typeahead" 
        >{{computedLocationTypeahead}}</span>
        <input 
            v-show="isComponentFocused"
            type="text"
            @focus="isLocationFocused = true"
            @blur="isLocationFocused = false"
            autocomplete="off"
            id="location-input"
            class="input"
            :placeholder="locationPlaceholder"
            v-model="location"
        >
        <ul v-show="serviceSuggestions && isServiceFocused" class="suggestions">
        <li v-for="suggestion in serviceSuggestions"
            tabindex="0"
            :key="suggestion"
            class="suggestion"
            @mousedown="()=>{ search({service: suggestion}) }"

        >{{suggestion}}</li>
        </ul>
        <ul v-show="locationSuggestions && isLocationFocused" class="suggestions">
        <li v-for="suggestion in locationSuggestions"
            tabindex="0"
            :key="suggestion"
            class="suggestion"
            @mousedown="()=>{ search({location: suggestion}) }"

        >{{suggestion}}</li>
        </ul>
    </div>
</template>

<script>
export default {
  name: 'YelpSearchMobile',
  props:{
    value: {
      type: Object,
      default: function () {
        return {
          service: "",
          location: ""
        }
      },
    },

    servicePlaceholder: {
      type: String,
      default: ""
    },

    serviceTypeahead: {
      type: String,
      default: ""
    },

    locationPlaceholder: {
      type: String,
      default: ""
    },

    locationTypeahead: {
      type: String,
      default: ""
    },

    serviceSuggestions: {
      type: Array,
      default: function () {
        return []
      }
    },

    locationSuggestions: {
      type: Array,
      default: function () {
        return []
      }
    }
  },

  data: function () {
    const vm = this;
    return {
      isComponentFocused: false,
      service: vm.value.service,
      location: vm.value.location,
      isServiceFocused: false,
      isLocationFocused: false,
      isSearching: false
    }
  },

  computed: {
    computedServiceTypeahead(){
      let typeahead = ""

      if(this.service && this.serviceTypeahead){
        for (let index = 0; index < this.service.length; index++) {
          if(this.service[index].toLowerCase() === this.serviceTypeahead[index].toLowerCase()){
            typeahead += this.service[index];
          }else{
            return ""
          }
        }

        for (let index = this.service.length; index < this.serviceTypeahead.length; index++) {
          typeahead += this.serviceTypeahead[index]
        }
      }

      return typeahead;
    },
    
    computedLocationTypeahead(){
      let typeahead = ""
      
      if(this.location && this.locationTypeahead){
        for (let index = 0; index < this.location.length; index++) {
          if(this.location[index].toLowerCase() === this.locationTypeahead[index].toLowerCase()){
            typeahead += this.location[index];
          }else{
            return ""
          }
        }

        for (let index = this.location.length; index < this.locationTypeahead.length; index++) {
          typeahead += this.locationTypeahead[index]
        }
      }

      return typeahead;
    }
  },

  methods: {
    search(input){
      const vm = this;
      if(vm.isSearching === true) return;
      vm.isSearching = true;
      console.log(input)
      const service = input.service || vm.service;
      const location = input.location || vm.location;
      vm.service = service;
      vm.location = location;
      vm.$emit("search",{service, location});

    //   if(vm.isServiceFocused){
    //       setTimeout(()=>{
    //           vm.isServiceFocused = true
    //       },0)
    //   }

    //   if(vm.isLocationFocused){
    //       setTimeout(()=>{
    //           vm.isLocationFocused = true
    //       },0)
    //   }

    //   setTimeout(()=>{
    //       vm.isComponentFocused = true
    //   },1)
    },

    handleFocus(isFocused){
        if(this.isSearching) return;
        this.isComponentFocused = isFocused
    }

  },

  watch: {
    service(userInput){
      this.$emit('input',{service: userInput, location: this.location});
    },

    location(userInput){
      this.$emit('input',{service: this.service, location: userInput});
    }
  },

  mounted(){
    const vm = this;
    const component = vm.$refs.container;
    document.addEventListener("focusin",()=> vm.handleFocus(component.contains(document.activeElement)))
    // document.addEventListener("focusout",()=>vm.handleFocus(component.contains(document.activeElement)))
    document.addEventListener('focusout',()=>{
        setTimeout(()=>{
            vm.handleFocus(component.contains(document.activeElement))
        },0)
    })
  }
}
</script>

<style scoped>
.container{
    display: inline-grid;
    font-size: 1.1rem;
    /* font-family: 'Courier New', Courier, monospace; */
    /* grid-template-rows: 1fr 1px 1fr 1fr; */
}

.suggestions{
  grid-row:4;
  grid-column: 1;
  font: inherit;
  vertical-align: baseline;
  border-radius: 0 0 4px 4px;
  box-shadow: 0 21px 38px rgb(0 0 0 / 20%);
  margin-top: 0!important;
  border-top: none;
  background-color: #fff;
  padding: 0;
  line-height: 1.28571em;
  font-size: 0.9rem;
  margin: -2rem 0 0;
  list-style: none;
  max-height: 400px;
  overflow-y: auto; 
}

.suggestion{
  padding: 0.5rem 1rem;
  color: #000;
  cursor: pointer;
  font-size: 0.9rem;
}

.input, .typeahead{
    padding: 0.2rem 0.2rem 0.2rem 40px;
    background-image: url('../assets/magnifying.mobile.svg');
    background-position: 3px 1px;
    background-repeat: no-repeat;
    text-indent: 0px;
    text-align: start;
    margin:0em;
    box-sizing: border-box;
    letter-spacing: normal;
    word-spacing: normal;
    line-height: normal;
    border-radius: 4px;
    width: 100%;
    margin: 0;
    border: 0;
    outline: 0;
    margin-bottom: -1px;
    /* border-width: 2px;
    border-style: inset;
    border-color: -internal-light-dark(rgb(118, 118, 118), rgb(133, 133, 133)); */
    font-family: inherit;
	font-size: 100%;
    overflow: hidden;
    /* background-color: #fff; */
}

.typeahead{
    pointer-events: none;
    /* background-color: #fff; */
    opacity: 0.6;;
}

.input{
    color: #000;
    background-color: #fff ;
}

#service-input, #service-typeahead{
    grid-row: 1;
    grid-column: 1;
    border-bottom-left-radius: 0;
    border-bottom-right-radius: 0;
}

.unfocused-service{
    border-bottom-left-radius: 4px !important;
    border-bottom-right-radius: 4px !important;
}

#location-input, #location-typeahead{
    grid-row: 3;
    grid-column: 1;
    border-top-left-radius: 0;
    border-top-right-radius: 0;
}

.suggestion:hover{
  background-color:#4682B4;
  color: #fff;
}

#line-break{
    grid-column: 1;
    grid-row: 2;
    content: "";
    height: 1px !important;
    width: 100%;
    margin: 0 ;
    background-color: #ccc;
}

</style>