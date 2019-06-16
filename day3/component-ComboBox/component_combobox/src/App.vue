<template>
 <div id="app">
   <ComboBox v-for="(item,index) in comboBoxItems"
            :key="index"
            :category="item.name"
            :v-model="item.selectIndex"
            :item-source="item.itemSource"
            v-on:input="onComboBoxSelected">
   </ComboBox>
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
  return cityData.getCities();
}

let getAreas = function(){
  return cityData.getAreas(this.selectCityIndex);
}

let getZipCode = function(){   
  return cityData.getZipCode(
    this.comboBoxItems[0].selectIndex
    ,this.comboBoxItems[1].selectIndex);
}

let mounted = function(){
  this.comboBoxItems[0].itemSource = cityData.getCities();
  this.comboBoxItems[1].itemSource 
    = cityData.getAreas(this.comboBoxItems[0].selectIndex,this.comboBoxItems[1].selectIndex );
}

export default {
  name: 'app',
  components: {
    ComboBox
  },
  data () {
    return {
      comboBoxItems:[
        {
          name:STRING_CITY,
          selectIndex : 0,
          itemSource : []
        },
        {
           name:STRING_AREA,
           selectIndex : 0,
           itemSource : []
        }
      ]
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
        switch(category)
        {
          default:break;
          case STRING_CITY:
            this.selectCityIndex = value;
            this.comboBoxItems[0].selectIndex = value;
          
            this.comboBoxItems[1].itemSource =
                cityData.getAreas( value);
            this.comboBoxItems[1].selectIndex = 0;
            break;

          case STRING_AREA:
            this.comboBoxItems[1].selectIndex = value;
            break;
        }
    },
  },
  mounted
}
</script>
