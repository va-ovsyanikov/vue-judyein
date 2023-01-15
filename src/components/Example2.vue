<template>
  <div class="hello">
    <h1>Example 2</h1>
    <input @click="send" type="button" value="Send" />
    <div v-if="loading">Загрузка...</div>
    <div class="out" v-if="successIds.length">{{ successIds }}</div>
  </div>
</template>

<script>

/*
@return
  resolve: { id: 1, success: true }
  or
  reject: { success: false }
*/
const fakeApiRequest = (id) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = id % 2 > 0;
      success ? resolve({ id, success }) : reject({ success });
    }, 2000);
  })
}

export default {
  data() {
    return {
      // Fetch ids
      ids: [1, 2, 3, 4, 5, 6],
      // Complete ids
      successIds: [],
      loading: false
    }
  },

  methods: {
    send() {
      let promises = []
      for (let item of this.ids) {
        this.loading = true
        promises.push(fakeApiRequest(item))
      }
      Promise.allSettled(promises).then(res => {
        let result = [];
        for (let item of res) {
          if (item.status === 'fulfilled') {
            result.push(item.value)
          }
        }
        this.$set(this, 'successIds', [...result]);
        this.loading = false
      }).catch(err => {
        console.log(err);
      })
    },
  }
};
</script>

<style scoped>
.hello{
  margin-bottom: 50px;
}
.out {
  margin: 20px 0;
  color: #41b883;
}
</style>