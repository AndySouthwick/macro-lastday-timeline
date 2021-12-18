<script>
import Swiper from "swiper"
import MacroLastDayTimeLine from "./../../json/macroLastDaysTimeline.json"
export default {
  name: "MacroLastDaysTimeline",
  props: {
    msg: String,
  },
  data() {
    return {
      macroLastDayTimeline: MacroLastDayTimeLine,
      selectedData: ""
    };
  },
  methods:{
    selectItem(data){
      this.selectedData = data
    }
  },
   mounted() {
     new Swiper('.swiper-container', {
      pagination: '.swiper-pagination',
      slidesPerView: 1,
      grabCursor: true,
      paginationClickable: true, 
      nextButton: '.next-slide',
      prevButton: '.prev-slide',
    });    
  }
};
</script>
<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="swiper-container">
          <div class="swiper-wrapper timeline">

            <div class="swiper-slide" v-for="(item, index) in macroLastDayTimeline.macroTimeLine" :key="index">
              <div class="timestamp">
                <span class="date">{{ macroLastDayTimeline.timeLineItems[item].title }}</span>
              </div>
              <div class="status">
                <span @click="selectItem(macroLastDayTimeline.timeLineItems[item])"></span>
              </div>
            </div>
          </div>
          <!-- Add Pagination -->
          <div class="swiper-pagination"></div>
        </div>
      <h2>{{selectedData.title}}</h2>
      <p>{{selectedData.description}}</p>
      <div v-for="(event, index) in selectedData.events" :key="index">
          <h3>{{event.eventName}}</h3>
          <ul>
            <li v-for="(sourceItem, sourceidx) in event.sources" :key="sourceidx"><a  :href="sourceItem.ref">{{sourceItem.source}}</a></li>
          </ul>
      </div>
      </div>
    </div>
    <div>
    </div>
  </div>
</template>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body {
  background: #353535;
  color: #fff;
}
#app {
  padding: 50px 0;
}
a{
  color: #fff;
}
ul li {
    text-align: left;
}
.timeline {
  margin: 50px 0;
  list-style-type: none;
  display: flex;
  padding: 0;
  text-align: center;
}
.timeline li {
  transition: all 200ms ease-in;
}
.timestamp {
  width: 300px;
  margin-bottom: 20px;
  padding: 0px 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-weight: 100; 
}
.status {
  padding: 0px 40px;
  display: flex;
  justify-content: center;
  border-top: 4px solid #3e70ff;
  position: relative;
  transition: all 200ms ease-in ;
}
  
.status span {
  font-weight: 600;
  padding-top: 20px;
}
.status span:before {
  content: '';
  width: 25px;
  height: 25px;
  background-color: #e8eeff;
  border-radius: 25px;
  border: 4px solid #3e70ff;
  position: absolute;
  top: -15px;
  left: 42%;
  transition: all 200ms ease-in;
}
.swiper-control {
  text-align: right;
}
.row {
    text-align: left;
}
.swiper-container {
  width: 100%;
  overflow: hidden;
  padding: 0 20px 30px 20px;
}
.swiper-slide {
  width: 250px;
  text-align: center;
  font-size: 18px;
}
.swiper-slide:nth-child(2n) {
  width: 40%;
}
.swiper-slide:nth-child(3n) {
  width: 20%;
}
</style>
