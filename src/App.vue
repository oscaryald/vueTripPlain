<template>

  <section class="create_trip_plan w-100">
    <h2 class="h2 row ml-0 mr-0 h2--flexmode flex-nowrap">
      <div>Create <span>trip plan</span></div>
    </h2>
    <p><b>To get the most out of this event, we recommend that you follow a few simple steps. This will give you more networking opportunities and also get some bonuses.</b></p>
    <div class="trip_plan_title">
      <div class="plan_citys"><strong>Lviv</strong> – <strong>Odessa</strong> – <strong>Lviv</strong></div>
      <div class="plan_days">11-13.10.2018</div>
    </div>
    <div class="trip_plan_wrapper">
      <Transport />
      <div class="trip_plan_item">
        <div class="trip_plan_block_icon">
          <div class="plan-v__i-icon">
            <div><svg width="26" height="22" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 26 22"><path d="M318.50156,1929.79846l-1.1,-4.09998l3.3,-2.70001l-4.2,-0.20001l-1.5,-3.90002l-1.5,3.90002l-4.3,0.20001l3.3,2.70001l-1.1,4.09998l3.6,-2.29999zM323.60156,1923.59845c-0.39999,0.40002 -0.60001,0.90002 -0.60001,1.40002c0,0.5 0.2,1 0.60001,1.40002c0.40001,0.40002 0.89999,0.59998 1.39999,0.59998v4c0,0.5 -0.2,1 -0.60001,1.40002c-0.40001,0.40002 -0.89999,0.59998 -1.39999,0.59998h-16c-0.5,0 -1,-0.20001 -1.4,-0.59998c-0.4,-0.39996 -0.6,-0.90002 -0.6,-1.40002v-4c0.6,0 1,-0.20001 1.4,-0.59998c0.4,-0.39996 0.6,-0.90002 0.6,-1.40002c0,-0.5 -0.2,-1 -0.6,-1.40002c-0.4,-0.40002 -0.9,-0.59998 -1.4,-0.59998v-4c0,-0.5 0.2,-1 0.6,-1.40002c0.4,-0.40002 0.9,-0.59998 1.4,-0.59998h16c0.5,0 1,0.20001 1.39999,0.59998c0.39999,0.39996 0.60001,0.90002 0.60001,1.40002v4c-0.59999,-0.00006 -1,0.19995 -1.39999,0.59998z" transform="matrix(1,0,0,1,-302,-1915)" fill="#ffffff"></path></svg></div>
          </div>
          <div class="title">Event</div>
        </div>
        <div class="trip_plan_content">
          <div class="trip_plan_box table-box last_right">
            <div class="table-cell">
              <div class="event_list">
                <div class="list_inline_block">
                  <div class="list_inline_item"><span class="simple_icon date_range_orange"></span><span>07.09.18</span></div>
                  <div class="list_inline_item"><span class="simple_icon clock_orange"></span><span>18:30</span></div>
                  <div class="list_inline_item"><span class="simple_icon event_orange"></span><span class="event_name">Atlas Weekend - Greatest Music Festival In Ukraine</span></div>
                </div>
              </div>
            </div>
            <div class="table-cell"><a class="people people_list" href="#">
                <div class="last">+1370</div></a>
              <button class="btn_select jsSelectShipping" type="button"></button>
            </div>
          </div>
        </div>
      </div>
      <div class="trip_plan_item">
        <div class="trip_plan_block_icon">
          <div class="plan-v__i-icon">
            <div><svg style="transform:scale(1.4)" width="29" height="29" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 38.87 38.869"><path d="M389.6 745.8l-7.579-2.5v5.5l1.895 1.5v1.5l-3.316-1-3.316 1v-1.5l1.895-1.5v-5.5l-7.579 2.5v-2l7.579-5v-5.5a1.554 1.554 0 0 1 .379-1.1 1.557 1.557 0 0 1 2.084 0 1.409 1.409 0 0 1 .379 1.1v5.5l7.579 5z" transform="rotate(-45 -673.158 816.081)" fill="#fff"></path></svg></div>
          </div>
          <div class="title">Transport from</div>
        </div>
        <div class="trip_plan_content">
          <div class="trip_plan_box table-box last_right">
            <div class="table-cell">
              <div class="trip_plan_found"><span class="label">Found:</span>
                <ul>
                  <li><span class="simple_icon train_icon_gray"></span><span class="number_wrap">(<span class="number">0</span>)</span></li>
                  <li><span class="simple_icon bus_icon_gray"></span><span class="number_wrap">(<span class="number">0</span>)</span></li>
                  <li><span class="simple_icon car_icon_gray"></span><span class="number_wrap">(<span class="number">0</span>)</span></li>
                  <li><span class="simple_icon airplane_icon_gray"></span><span class="number_wrap">(<span class="number">0</span>)</span></li>
                </ul>
              </div>
              <div class="trip_plan_info">
                <ul>
                  <li><span>Travelmates: </span><strong>133</strong></li>
                  <li><span>Friends: </span><strong>0</strong></li>
                </ul>
              </div>
            </div>
            <div class="table-cell">
              <button class="btn_select jsSelectShipping" type="button">Select Shipping</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Transport from "./components/Transport";
import { apiUrl } from "./components/api-url/ApiUrl";

export default {
  name: 'app',
  components: {
    Transport,
  },
}
</script>

<style lang="scss">
p{
  margin-bottom: 20px;
}
.trip_plan_content_inner {
  display: block;
}
</style>
