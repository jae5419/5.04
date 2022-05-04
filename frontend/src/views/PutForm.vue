<template>
  <div>
    <h1>글을 수정하는 곳입니다</h1>
    <input type="text" v-model="memo.title"><br>
    <textarea cols="30" rows="10" v-model="memo.memo"></textarea><br>
    <button @click="update(memo.id)">수정</button>
  </div>
</template>

<script>
export default {
  data() {
    return ({
      memo: {}
    })
  },
  created() {
    this.$http.get(`/api/memo/${this.$route.params.id}`)
    .then((res) => {
      this.memo=res.data;
    })
  },
  methods: {
    update: function(id) {
      this.$http.put(`/api/memo/${id}`, {
        data: {
          title: this.memo.title,
          memo: this.memo.memo
        }
      })
      .then((res) => {
        console.log(res.data);
        this.$router.push('/');
      })
    }
  }
}
</script>