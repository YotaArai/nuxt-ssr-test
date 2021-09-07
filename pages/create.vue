<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-form ref="form" v-model="valid" @submit.prevent="post">
        <v-text-field
          name="content"
          label="内容"
          v-model="content"
          :counter="contentCount"
          :rules="contentRule"
        ></v-text-field>
        <v-btn type="submit" large rounded :disabled="!valid"> 投稿 </v-btn>
      </v-form>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      valid: false,
      content: "",
      contentCount: 50,
      contentRule: [
        (v) => !!v || "入力してください",
        (v) =>
          v.length <= this.contentCount ||
          "入力できるのは" + this.contentCount + "文字までです",
      ],
    };
  },
  methods: {
    post() {
      const url = "https://echo-test-ya.herokuapp.com/posts";
      let params = new FormData();
      params.append("content", this.content);
      this.$axios.$post(url, params).then((response) => {
        location.href = "/";
      });
    },
  },
};
</script>