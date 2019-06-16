<template>
 <div id="app">
   <combo-box id="comboBoxCities"  
              :category="categoryCity"
              :v-model="selectCityIndex"
              :item-source="getCities"
              v-on:input="onComboBoxSelected" ></combo-box>
   <ComboBox id="comboBoxAreas" 
             :category="categoryArea"
             :v-model="selectAreaIndex"
             :item-source="getAreas" 
             v-on:input="onComboBoxSelected"></ComboBox>
   <span>{{getZipCode}}</span>
 </div>
</template>

<script>


import ComboBox from './components/ComboBox'
import cityData from './models/cities'
import { log } from 'util';

const STRING_CITY ="city";
const STRING_AREA ="area";

let getCities = function(){
  return this.cities.map(city=>city.name);
}

let getAreas = function()
{
   let city = this.cities[this.selectCityIndex];

   if (!city) 
      return [];

    return city.areas.map(area => area.name);
}

let getZipCode = function()
{   
  let city = this.cities[this.selectCityIndex];
  if (!city)
   return "";
  let area = city.areas[this.selectAreaIndex];
  if(!area)
    return "N/A";
  let zipCode = area.zip;
  return  zipCode;
}

export default {
  name: 'app',
  components: {
    ComboBox
  },
  data () {
    return {
      cities : cityData.cities ,
      categoryCity: STRING_CITY,
      categoryArea:STRING_AREA,
      selectCityIndex: 1,
      selectAreaIndex : 0,
    }
  },
  computed:{
    getCities,
    getAreas,
    getZipCode,
  },
  methods:{
    onComboBoxSelected : function(category, value)
    {
        console.log("enter onComboBoxSelected");
        console.log(category);
        console.log(value);
        switch(category)
        {
          default:break;
          case STRING_CITY:
            this.selectCityIndex = value;
            this.selectAreaIndex = 0;
            break;
          case STRING_AREA:
            this.selectAreaIndex =value;
            break;
        }
    },
  }
}
</script>
