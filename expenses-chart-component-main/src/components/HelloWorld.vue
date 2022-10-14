<template>
  <div class="flex flex-col justify-center items-center w-full gap-4">
    <!-- header -->
    <div
      class="flex justify-between items-center bg-softred h-[5rem] w-[90%] md:w-[35%] rounded-[15px] p-4"
    >
      <div>
        <p class="text-white text-sm font-thin">My Balance</p>
        <p class="text-white text-xl font-bold">$921.48</p>
      </div>
      <svg
        width="72"
        height="48"
        viewBox="0 0 72 48"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g fill="none" fill-rule="evenodd">
          <circle fill="#382314" cx="48" cy="24" r="24" />
          <circle stroke="#FFF" stroke-width="2" cx="24" cy="24" r="23" />
        </g>
      </svg>
    </div>

    <div
      class="charts-body flex flex-col justify-between h-[25rem] w-[90%] md:w-[35%] rounded-[15px] p-4"
    >
      <!-- title chart -->
      <h1 class="font-bold text-2xl">Spending - Last 7 days</h1>
      <!-- body charts -->
      <div class="flex justify-between items-end h-[8.125rem]">
        <div
          v-for="(item, index) in data"
          :key="item.day"
          class="flex flex-col justify-center items-center w-[50px] align-center"
        >
          <div
            v-if="item.hovered"
            class="flex justify-center items-center bg-[#382314] rounded-lg mb-[5px] h-[30px] w-full p-4"
          >
            <p class="text-white text-center text-sm">${{ item.amount }}</p>
          </div>
          <div
            class="bg-softred rounded-md w-[80%]"
            @mouseover="hoverChart(index)"
            @mouseleave="leaveChart(index)"
            v-bind:class="{
              today: item.isToday,
              chartStick: item.hovered,
            }"
            v-bind:style="{ height: item.amount * 2 + 'px' }"
          ></div>
          <p class="text-center">{{ item.day }}</p>
        </div>
      </div>
      <span class="w-full border-b-[1px] border-[#93867b]"></span>
      <!-- footer chart -->
      <div class="flex justify-between items-center rounded-[15px] p-4">
        <div>
          <p class="text-[#93867b] text-sm font-thin">Total This Month</p>
          <p class="text-4xl font-bold">${{ this.total }}</p>
        </div>
        <div></div>
        <div>
          <p class="text-sm text-end font-bold">+24%</p>
          <p class="text-[#93867b] text-sm font-thin">From Last Month</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import data from "../data.json";
export default {
  data() {
    return {
      data,
      total: 0,
    };
  },

  name: "HelloWorld",
  props: {
    msg: String,
  },

  created() {
    const day = new Date().getDay() - 1;

    for (let i = 0; i < this.data.length; i++) {
      this.total += this.data[i].amount;
      this.data[i].isToday = false;
      Vue.set(this.data[i], "hovered", false);
      if (day == i) this.data[i].isToday = true;
      if (i >= this.data.length) return;
    }
    console.log(this.data);
  },

  methods: {
    getChartHeight(amount) {
      console.log(`h-[${amount}px] bg-softred rounded-md w-full`);
    },
    hoverChart(index) {
      this.data[index].hovered = true;
    },
    leaveChart(index) {
      this.data[index].hovered = false;
      // Vue.set(this.data, index, true);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.chartStick {
  opacity: 60%;
}
.today {
  background-color: hsl(186, 34%, 60%);
}
.charts-body {
  background-color: white;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
