<template>
  <div class="progress">
    <div
     
      :class="activeClass"
      role="progressbar"
      :style="{width: progressbarWidth +'%'}"
      aria-valuenow="50"
      aria-valuemin="0"
      aria-valuemax="100"
    >
      {{ productCount }}/10
    </div>
  </div>
</template>

<script>
import {eventBus} from "../main";
export default {
  data() {
    return {
      productCount: 0,
      progressbarWidth: 0,
      activeClass : "progress-bar bg-info"
    };
  },
  created() {
    eventBus.$on("progressbarUpdated", (count) => {
      
      this.productCount = count;
      this.progressbarWidth = count * 10;
      if (count>5){
        this.activeClass="progress-bar bg-danger"
      }
     
    });
  },
};
</script>
