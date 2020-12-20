<template>
  <header class="mb-3">Comment List with json-server</header>

  <div class="container">
    <div class="row">
      <div class="col-4">
        <h2>Add Comment</h2>
        <hr />
        <div class="input-group input-group-sm mb-3">
          <input
            type="text"
            class="form-control"
            aria-label="Sizing example input"
            aria-describedby="inputGroup-sizing-sm"
            placeholder="Type your Comment..."
            v-model="commentData.desc"
          />
          <button type="button" class="btn btn-primary btn-sm ml-1" @click="addComment">
            Comment
          </button>
        </div>
      </div>
      <div class="col-8">
        <comment-list :commentList="commentList" />
      </div>
    </div>
  </div>
</template>

<script>

import CommentList from "./components/CommentList";
import axios from "axios";
export default {
  name: "App",
  components: {

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
  created(){
    axios.get('http://localhost:3000/comments').then((response) => {
      this.commentList = response.data
    }).catch((e) => {
      alert(e)
    })
  },
  methods : {
    addComment(){
      axios.post('http://localhost:3000/comments', this.commentData).then((response) => {
      if (response.status === 201){
        this.commentList.push(response.data)
      };
      this.commentData = {
        desc : null,
      }
      
      })
    }
  }
}
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
