<template>
  <div class="trip_plan_item">
    <div class="trip_plan_block_icon">
      <div class="plan-v__i-icon">
        <div><svg width="22" height="22" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 22 22"><path d="M318.96989,1063.82217l-3.59136,-7.12689l-3.88909,3.88909l0.27913,2.40045l-1.06066,1.06066l-1.63751,-3.05173l-3.05173,-1.63751l1.06066,-1.06066l2.40045,0.27913l3.88909,-3.88909l-7.12689,-3.59136l1.41421,-1.41421l8.89466,1.82359l3.88909,-3.88909c0.28286,-0.28286 0.63268,-0.49867 1.04575,-0.50985c0.41309,-0.01116 0.68479,0.11907 1.01975,0.45403c0.33495,0.33495 0.4652,0.60659 0.45403,1.01975c-0.01118,0.41316 -0.1563,0.6922 -0.50985,1.04575l-3.88909,3.88909l1.82359,8.89466z" fill="#fff" transform="matrix(1,0,0,1,-304,-1045)"></path></svg></div>
      </div>
      <div class="title">Transport to</div>
    </div>
    <div class="trip_plan_content">
      <div class="trip_plan_box table-box last_right">
        <div class="table-cell">
          <div class="trip_plan_found"><span class="label">Found:</span>
            <ul>
              <li
                v-for="(item, index) in items"
                :key="index"
              >
              <span :class="`simple_icon ${item.value}_icon_gray`"></span>
                  <template v-if="item.value === 'car'">
                    <span class="number_wrap">(<span class="number">{{cars.length}}</span>)</span>
                  </template>
                  <template v-else>
                    <span class="number_wrap">(<span class="number">0</span>)</span>
                  </template>
              </li>
            </ul>
          </div>
          <div class="trip_plan_info">
            <ul>
              <li><span>Travelmates: </span><strong>213</strong></li>
              <li><span>Friends: </span><strong>7</strong></li>
            </ul>
          </div>
        </div>
        <div class="table-cell">
          <button class="btn_select" type="button" @click="isOpen = !isOpen">Select Shipping</button>
        </div>
        
      </div>
      <div class="trip_plan_content_inner" v-show="isOpen">
        <div class="trip_plan_search_form">
          <div class="list_inline_block last_right">
            <div class="list_inline_item">
              <input @input="autocompliteCity(fromCity, 'selectedCityFrom')" v-model="fromCity" class="form_control plan_from" type="text" placeholder="City">
              <ul class="autocomplite" v-if="selectedCityFrom.length">
                <li v-for="(item, index) in selectedCityFrom" :key="index" @click="selectCity('fromCity', item)">
                  {{item.value}}
                </li>
              </ul>
            </div>
            
            <div class="list_inline_item">
              <button class="btn btn_change" type="button"></button>
            </div>
            <div class="list_inline_item">
              <input @input="autocompliteCity(toCity, 'selectedCityTo')" v-model="toCity" class="form_control plan_to" type="text" placeholder="City">
              <ul class="autocomplite" v-if="selectedCityTo.length">
                <li v-for="(item, index) in selectedCityTo" :key="index"  @click="selectCity('toCity', item)">
                  {{item.value}}
                </li>
              </ul>
            </div>
            <div class="list_inline_item">
              <date-picker class="form_control plan_date" type="text" v-model="datepicker" lang="en" :not-before="new Date()"></date-picker>
            </div>
          </div>
          <div class="block_btn">
            <button @click="search" class="btn btn--orange btn_search" type="button">SEARCH</button>
          </div>
        </div>
        
        <div class="trip_plan_all_steps">
          <div class="tabs">
            <div class="tabs__tabs">
              <div
                :class="{'tabs__tab': true, '-active': currentTab === tab.value}"
                v-for="(tab, index) in items"
                :key="index"
                :data-tab="index"
                @click="currentTab = tab.value"
              >
                <div class="tabs_title">
                  <span :class="`simple_icon ${tab.value}_icon_gray`"></span>
                  {{tab.title}}
                  <template v-if="tab.value === 'car'">
                    (<span>{{cars.length}}</span>)
                  </template>
                  <template v-else>
                    (<span>7</span>)
                  </template>
                </div>
              </div>
            </div>
            <div class="tabs__content">
              <div
                :class="{'tabs__item': true, '-fade': currentTab === tab.value, '-active': currentTab === tab.value}"
                v-for="(tab, index) in items"
                :key="index"
              >
                <template v-if="tab.value === 'all'">
                  <div class="plan_info">
                    <div class="plan_item">
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon train_icon_gray"></span><span>128ВШ</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>Lviv test test test test test test test</span></li>
                              <li class="plan_time">13 July 2018<strong>18:37</strong></li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>Odesa-Holovna</span></li>
                              <li class="plan_time">14 July 2018<strong>06:42</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_reserved">
                              <li>reserved:<strong>213</strong></li>
                              <li>reserved:<strong>85</strong></li>
                              <li>reserved:<strong>124</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>165 - 1650 </strong><span>uah</span></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                      <div class="plan_info_bottom">
                        <div class="table-box last_right plan_info_bottom_wrapper">
                          <div class="table-cell">
                            <div class="list_inline_block">
                              <div class="list_inline_item">
                                <div class="trip_plan_info">
                                  <ul>
                                    <li><span>Travelmates: </span><strong>13</strong></li>
                                  </ul>
                                </div>
                              </div>
                              <div class="list_inline_item"><a class="people people_list" href="#">
                                  <div class="last">+1370</div></a></div>
                            </div>
                          </div>
                          <div class="table-cell">
                            <button class="btn btn-be-here" type="button">I'l be here</button>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="plan_item">
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon train_icon_gray"></span><span>128ВШ</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>Lviv</span></li>
                              <li class="plan_time">13 July 2018<strong>18:37</strong></li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>Odesa-Holovna</span></li>
                              <li class="plan_time">14 July 2018<strong>06:42</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_reserved">
                              <li>first:<strong>213</strong></li>
                              <li>second:<strong>85</strong></li>
                              <li>third:<strong>124</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>165 - 1650 </strong><span>uah</span></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="plan_item">
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon bus_icon_gray"></span><span>PS-36</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>Lviv</span></li>
                              <li class="plan_time">13 July 2018<strong>18:37</strong></li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>Odesa-Holovna</span></li>
                              <li class="plan_time">14 July 2018<strong>06:42</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item"></div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>3686 </strong><span>uah</span></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="plan_item">
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon car_icon_gray"></span><span>PS-36</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>Lviv</span></li>
                              <li class="plan_time">13 July 2018<strong>18:37</strong></li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>Odesa-Holovna</span></li>
                              <li class="plan_time">14 July 2018<strong>06:42</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item"></div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>3686 </strong><span>uah</span></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="plan_item">
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon airplane_icon_gray"></span><span>PS-36</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>Lviv</span></li>
                              <li class="plan_time">13 July 2018<strong>18:37</strong></li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>Odesa-Holovna</span></li>
                              <li class="plan_time">14 July 2018<strong>06:42</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item"></div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>3686 </strong><span>uah</span></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="text-center"><a class="load-more" href="#">
                      <svg width="16" height="22" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 22"><path d="M8 3V0L4 4l4 4V5a6 6 0 0 1 6 6 5.87 5.87 0 0 1-.7 2.8l1.46 1.46A7.986 7.986 0 0 0 8 3zm0 14a6 6 0 0 1-6-6 5.87 5.87 0 0 1 .7-2.8L1.24 6.74A7.986 7.986 0 0 0 8 19v3l4-4-4-4z"></path></svg>
                      Load more</a></div>
                </template>

                <template v-else-if="tab.value === 'train'">
                  <div class="plan_info">
                    <div class="plan_item">
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon train_icon_gray"></span><span>128ВШ</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>Lviv</span></li>
                              <li class="plan_time">13 July 2018<strong>18:37</strong></li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>Odesa-Holovna</span></li>
                              <li class="plan_time">14 July 2018<strong>06:42</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_reserved">
                              <li>first:<strong>213</strong></li>
                              <li>second:<strong>85</strong></li>
                              <li>third:<strong>124</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>165 - 1650 </strong><span>uah</span></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="text-center"><a class="load-more" href="#">
                      <svg width="16" height="22" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 22"><path d="M8 3V0L4 4l4 4V5a6 6 0 0 1 6 6 5.87 5.87 0 0 1-.7 2.8l1.46 1.46A7.986 7.986 0 0 0 8 3zm0 14a6 6 0 0 1-6-6 5.87 5.87 0 0 1 .7-2.8L1.24 6.74A7.986 7.986 0 0 0 8 19v3l4-4-4-4z"></path></svg>
                      Load more</a></div>
                </template>

                <template v-else-if="tab.value === 'bus'">
                  <div class="plan_info">
                    <div class="plan_item">
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon bus_icon_gray"></span><span>PS-36</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>Lviv</span></li>
                              <li class="plan_time">13 July 2018<strong>18:37</strong></li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>Odesa-Holovna</span></li>
                              <li class="plan_time">14 July 2018<strong>06:42</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item"></div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>3686 </strong><span>uah</span></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="text-center"><a class="load-more" href="#">
                      <svg width="16" height="22" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 22"><path d="M8 3V0L4 4l4 4V5a6 6 0 0 1 6 6 5.87 5.87 0 0 1-.7 2.8l1.46 1.46A7.986 7.986 0 0 0 8 3zm0 14a6 6 0 0 1-6-6 5.87 5.87 0 0 1 .7-2.8L1.24 6.74A7.986 7.986 0 0 0 8 19v3l4-4-4-4z"></path></svg>
                      Load more</a></div>
                </template>

                <template v-else-if="tab.value === 'car'">
                  <div class="plan_info">
                    <div 
                      class="plan_item" 
                      v-for="(item, index) in cars"
                      :key="index"
                    >
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon car_icon_gray"></span><span>PS-36</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>{{item.departure_city}}</span></li>
                              <li class="plan_time">{{item.departure_date}}</li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>{{item.arrival_city}}</span></li>
                              <li class="plan_time">{{item.arrival_date}}</li>
                            </ul>
                          </div>
                          <div class="list_inline_item"></div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>{{item.price}}</strong></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="text-center"><a class="load-more" href="#">
                      <svg width="16" height="22" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 22"><path d="M8 3V0L4 4l4 4V5a6 6 0 0 1 6 6 5.87 5.87 0 0 1-.7 2.8l1.46 1.46A7.986 7.986 0 0 0 8 3zm0 14a6 6 0 0 1-6-6 5.87 5.87 0 0 1 .7-2.8L1.24 6.74A7.986 7.986 0 0 0 8 19v3l4-4-4-4z"></path></svg>
                      Load more</a></div>
                </template>

                <template v-else-if="tab.value === 'airplane'">
                  <div class="plan_info">
                    <div class="plan_item">
                      <div class="plan_info_top">
                        <div class="list_inline_block last_right">
                          <div class="list_inline_item">
                            <div class="plan_number"><span class="simple_icon airplane_icon_gray"></span><span>PS-36</span></div>
                          </div>
                          <div class="list_inline_item">
                            <ul class="plan_way">
                              <li><span>Lviv</span></li>
                              <li class="plan_time">13 July 2018<strong>18:37</strong></li>
                            </ul>
                            <ul class="plan_way">
                              <li><span>Odesa-Holovna</span></li>
                              <li class="plan_time">14 July 2018<strong>06:42</strong></li>
                            </ul>
                          </div>
                          <div class="list_inline_item"></div>
                          <div class="list_inline_item">
                            <div class="plan_price"><strong>3686 </strong><span>uah</span></div>
                          </div>
                          <div class="list_inline_item">
                            <button class="btn btn--buy-gray" type="button">Buy ticket</button>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="text-center"><a class="load-more" href="#">
                      <svg width="16" height="22" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 22"><path d="M8 3V0L4 4l4 4V5a6 6 0 0 1 6 6 5.87 5.87 0 0 1-.7 2.8l1.46 1.46A7.986 7.986 0 0 0 8 3zm0 14a6 6 0 0 1-6-6 5.87 5.87 0 0 1 .7-2.8L1.24 6.74A7.986 7.986 0 0 0 8 19v3l4-4-4-4z"></path></svg>
                      Load more</a></div>
                </template>
              
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { apiUrl } from "./api-url/ApiUrl";
import DatePicker from 'vue2-datepicker'

export default {
  name: 'Transport',
  components: {
    DatePicker,
  },
  data() {
    return {
      fromCity: '',
      toCity: '',
      selectedCityFrom: [],
      selectedCityTo: [],
      items: [
        {
          title: 'All',
          value: 'all',
        }, 
        {
          title: 'Train',
          value: 'train',
        }, 
        {
          title: 'Bus',
          value: 'bus',
        }, 
        {
          title: 'Car',
          value: 'car',
        },
        {
          title: 'Airplane',
          value: 'airplane',
        }
      ],
      currentTab: 'all',
      datepicker: '',
      isOpen: false,
      cars: [],
      searchParams: {},
    };
  },
  methods: {
    // 31-01-2019 12:30:00
    fetchCars(from='1',to='45307',date='30.01.2019'){
       fetch(`${apiUrl}api/transport/search-car?event_id=1492652&from=${from}&to=${to}&date=${date}&passenger=1&is_before=1`)
        .then(res =>res.json())
        .then(res => {
          console.log(res)
          this.cars = res;
        })
    },

    autocompliteCity(value, selectedCities) {
      if(value === '') {
        this[selectedCities] = [];
        return;
      };

      fetch(`${apiUrl}uk/new/city/autocomplete?q=${value}&withId=1`)
        .then(res => res.json())
        .then(cities => {
          this[selectedCities] = cities;
        });
    },

    selectCity(selectedCity, value) {
      this[selectedCity] = value.label;
      this.searchParams[selectedCity] = value.id;
      this.selectedCityFrom = [];
      this.selectedCityTo = [];
    },

    search() {
      
      const d = new Date(this.datepicker);
      const date = `${d.getUTCDate()}.${d.getUTCMonth() + 1}.${d.getUTCFullYear()}`;
      const params = {...this.searchParams, date};
      console.log(params)
      this.fetchCars(params.fromCity, params.toCity, params.date);
    }
  },
  created() {
    this.fetchCars();
  }
}
</script>
<style scoped lang="scss">
.list_inline_item{
  position: relative;
}
.autocomplite{
  position: absolute;
  left: 0;
  background: #fff;
  width: 100%;
  z-index: 10;

  li{
    padding: 10px;
    cursor: pointer;
  }
}

/deep/ .mx-input{
  box-shadow: none;
  border:none;
  height: max-content;
}

/deep/ .mx-input-append{
    height: 20px;
    padding: 0;
}

.trip_plan_search_form .plan_date {
    padding: 13px 30px 13px 40px;
}
</style>


