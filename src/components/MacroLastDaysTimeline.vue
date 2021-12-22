<script>
import { Swiper } from "swiper";
import MacroLastDayTimeLine from "./../../json/macroLastDaysTimeline.json";
export default {
  name: "MacroLastDaysTimeline",
  props: {
    msg: String,
  },
  data() {
    return {
      macroLastDayTimeline: MacroLastDayTimeLine,
      selectedData: "",
      showSectionData: null,
    };
  },
  methods: {
    selectItem(data) {
      this.selectedData = data;
    },
    openSection(index) {
      this.showSectionData = index;
    },
  },
  mounted() {
    const swiper = new Swiper(".swiper-container", {
      pagination: ".swiper-pagination",
      slidesPerView: 1,
      grabCursor: true,
      paginationClickable: true,
      nextButton: ".next-slide",
      prevButton: ".prev-slide",
      on: {
        init: (data) => {
          console.log("swiper initialized");
          this.selectedData =
            MacroLastDayTimeLine.timeLineItems[
              MacroLastDayTimeLine.macroTimeLine[data.activeIndex]
            ];
        },
      },
    });
    swiper.on("slideChange", (data) => {
      this.selectedData =
        MacroLastDayTimeLine.timeLineItems[
          MacroLastDayTimeLine.macroTimeLine[data.activeIndex]
        ];
    });
  },
};
</script>
<template>
  <div id="app" class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="swiper-container">
          <div class="swiper-wrapper timeline">
            <div
              class="swiper-slide"
              v-for="(item, index) in macroLastDayTimeline.macroTimeLine"
              :key="index"
            >
              <div class="timestamp">
                <span class="date">{{
                  macroLastDayTimeline.timeLineItems[item].title
                }}</span>
              </div>
              <div class="status">
                <span
                  @click="selectItem(macroLastDayTimeline.timeLineItems[item])"
                ></span>
              </div>
            </div>
          </div>
          <!-- Add Pagination -->
          <div class="swiper-pagination"></div>
        </div>
        <div class="content-wrapper">
          <div class="Conent">
            <h2>{{ selectedData.title }}</h2>
            <p>{{ selectedData.description }}</p>
            <div v-for="(event, index) in selectedData.events" :key="index">
              <div
                class="accordian-pannel"
                @click="openSection(`${event.eventName}-${index}`)"
              >
                <h3 class="Selectable">
                  {{ event.eventName }}
                </h3>
                <div class="down-arrow"></div>
              </div>
              <ul>
                <transition name="fade">
                  <div v-if="showSectionData == `${event.eventName}-${index}`">
                    <li
                      v-for="(sourceItem, sourceidx) in event.sources"
                      :key="`${sourceidx}-${sourceItem}`"
                    >
                      <a
                        :href="sourceItem.ref"
                        v-if="sourceItem.ref"
                        target="_blank"
                        >{{ sourceItem.source }}</a
                      >
                    </li>
                  </div>
                </transition>
                <transition name="fade">
                  <div v-if="showSectionData === `${event.eventName}-${index}`">
                    <li
                      v-for="(eventinevent, index) in event.events"
                      :key="`${eventinevent}-${index}`"
                    >
                      <strong>{{ eventinevent.eventName }}</strong>
                      <ul>
                        <li
                          v-for="(source, index) in eventinevent.sources"
                          :key="index"
                        >
                          <a :href="source.ref" target="_blank">{{
                            source.source
                          }}</a>
                        </li>
                      </ul>
                    </li>
                  </div>
                </transition>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div></div>
  </div>
</template>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h3 {
  font-size: 1.1em;
}
.accordian-pannel {
  border-top: 2px solid #8d8c8cbd;
  display: flex;
  justify-content: space-between;
}
.accordian-pannel h3 {
  max-width: 300px;
}
.down-arrow {
  background-repeat: no-repeat;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='18' height='18' viewBox='0 0 72 72'%3E%3Cpath fill='none' stroke='%23ffffff' stroke-width='3.8' stroke-linecap='round' stroke-linejoin='round' stroke-miterlimit='10' d='M62 22.48L36.008 49.52 10 22.48'%3E%3C/path%3E%3C/svg%3E");
  width: 18px;
  height: 18px;
  margin-top: 20px;
}
.content-wrapper {
  display: flex;
  justify-content: center;
  align-content: center;
  align-items: center;
  width: 100vw;
  padding-left: 11px;
}
.Selectable {
  cursor: pointer;
}
.Conent {
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
}
.Conent h2 {
  text-align: center;
}
body {
  background: #353535;
  color: #fff;
}
#app {
  padding: 50px 0;
}
a {
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
  transition: all 200ms ease-in;
}

.status span {
  font-weight: 600;
  padding-top: 20px;
}
.status span:before {
  content: "";
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
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
