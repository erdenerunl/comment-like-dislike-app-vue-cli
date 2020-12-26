<template>
  <div>
    <div class="container">
      <h2>Comment List</h2>
      <hr />
      <div class="card mb-2" v-for="comment in commentList" :key="comment.id">
        <div class="card-body">
          <p class="card-text">
            {{ comment.desc }}
          </p>
          <div class="container text-right">
            <button
              type="button"
              class="btn btn-success btn-sm mr-1"
              @click="isLike(comment)"
            >
              Like {{ comment.like }}
            </button>
            <button
              @click="disLike(comment)"
              type="button"
              class="btn btn-danger btn-sm"
            >
              Dislike {{ comment.dislike }}
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["commentList"],
  methods: {
    isLike(comment) {
      
      const matchedComment = this.commentList.findIndex(
        (b) => b.id === comment.id
      );
      this.commentList[matchedComment].like++;
      axios
        .patch(
          `http://localhost:3000/comments/${comment.id}`,
          this.commentList[matchedComment]
        )
        .catch((e) => alert(e));
    },
    disLike(comment) {
      
      const matchedComment = this.commentList.findIndex(
        (b) => b.id === comment.id
      );
      this.commentList[matchedComment].dislike++
      axios
        .patch(
          `http://localhost:3000/comments/${comment.id}`,
          this.commentList[matchedComment]
        )
        .catch((e) => alert(e));
    },
  },
};
</script>