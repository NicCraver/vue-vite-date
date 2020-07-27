<template>
  <div>
    <div id="date">{{ remaining }}</div>
    <div id="timer">{{ Time }}:{{ Minute }}:{{ second }}</div>
  </div>
</template>

<script>
import { ref, reactive, toRefs, onMounted, computed } from "vue";
export default {
  setup() {
    const state = reactive({
      remaining: "",
      Time: "",
      Minute: "",
      second: "",
    });
    onMounted(() => {
      clock(state);
      setInterval(() => {
        clock(state);
      }, 1000);
    });
    return { ...toRefs(state) };
  },
};
function clock(state) {
  var H = new Date().getHours();
  H = H > 9 ? H : "0" + H;
  var M = new Date().getMinutes();
  M = M > 9 ? M : "0" + M;
  var S = new Date().getSeconds();
  S = S > 9 ? S : "0" + S;
  state.remaining = getDate();
  state.Time = H;
  state.Minute = M;
  state.second = S;
}
function getDate(dates) {
  var dd = new Date();
  var n = dates || 0;
  dd.setDate(dd.getDate() + n);
  var y = dd.getFullYear();
  var m = dd.getMonth() + 1;
  var d = dd.getDate();
  m = m < 10 ? "0" + m : m;
  d = d < 10 ? "0" + d : d;
  var day = y + "年" + m + "月" + d + "日";
  return day;
}
</script>
