<template>
  <div>
    <h1>Example 1</h1>
    <div v-for="(a, i) in arr" :key="i" :class="{ 'checked': a }" @click="toggleItem(i)" class="checkbox"></div>
    <div class="out">{{ arr }}</div>
    <input @click="resetState" type="button" value="Reset" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      arr: [true, false, true, false, true, true, true],
    }
  },
  methods: {
    toggleItem(index) {
      this.arr.splice(index, 1, !this.arr[index])
    },
    resetState() {
      if (localStorage.getItem("arr")) {
        try {
          this.arr = []
          for(const item of JSON.parse(localStorage.getItem("arr"))){
            this.arr.push(item);
          }
        } catch (e) {
          localStorage.removeItem("arr");
        }
      }
    }
  },
  mounted() {
    localStorage.setItem('arr', JSON.stringify(this.arr));
  }
};
</script>


<style scoped>
.checkbox {
  display: inline-block;
  width: 16px;
  height: 16px;
  margin: 0 5px;
  border: 1px solid gray;
  cursor: pointer;
}

.checkbox.checked {
  background-image: radial-gradient(#41b883 3px, white 4px);
}

.out {
  margin: 20px 0;
}
</style>