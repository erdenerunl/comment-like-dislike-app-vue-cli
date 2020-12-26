<template>
  <header class="mb-3">Comment List with json-server</header>

  <div class="container">
    <div class="row">
      <div class="col-4">
        <add-comment @addComment="addComment($event)" :commentData="commentData"/>
      </div>
      <div class="col-8">
        <comment-list :commentList="commentList" />
      </div>
    </div>
  </div>
</template>

<script>
import AddComment from "./components/AddComment";
import CommentList from "./components/CommentList";
import axios from "axios";
export default {
  name: "App",
  components: {
    AddComment,
    CommentList,
  },
  data() {
    return {
      commentData: {
        desc: "",
        like: 0,
        dislike: 0,
      },
      commentList: [],
    };
  },
  created() {
    axios
      .get("http://localhost:3000/comments")
      .then((response) => {
        this.commentList = response.data;
      })
      .catch((e) => {
        alert(e);
      });
  },
  methods: {
    addComment() {
      axios
        .post("http://localhost:3000/comments", this.commentData)
        .then((response) => {
          if (response.status === 201) {
            this.commentList.push(response.data);
          }
          this.commentData = {
            desc: null,
          };
        });
    },
  },
};
</script>

<style>
header {
  font-size: 25px;
  text-align: center;
  background: #d2d2d2;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
