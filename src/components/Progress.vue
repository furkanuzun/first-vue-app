<template>
  <div class="progress">
      <div class="progress-bar bg-info" role="progressbar" :style="style" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100">
        {{ productListLength }}/10
      </div>
    </div>
</template>
<script>
import { eventBus } from "../main.js"

export default {
  data() {
    return {
      productListLength : 0,
      style : "width :0%"
    }
  },
  created(){
    eventBus.$on("productListLength", (length) => {
      this.productListLength = length;
      this.style = "width: " + length * 10 +"%";
    })
  }
}
</script>