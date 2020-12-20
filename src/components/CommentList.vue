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
              <button type="button" class="btn btn-success btn-sm mr-1" @click="isLike(comment)">Like {{ comment.like }} </button>
              <button type="button" class="btn btn-danger btn-sm">Dislike</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    props : ["commentList"],
    data(){
        return {
            updateId : null,
        }
    },
    methods : {
        isLike(comment){
            this.updateId = comment.id
            console.log(this.updateId, 'this.updateId')
            axios.patch(`http://localhost:3000/comments/${this.updateId}`, this.commentData.like)
            .then((response) =>{
                const matchedComment = this.commentList.findIndex((b) => b.id === this.updateId)
                this.commentList[matchedComment].like++
                console.log(this.commentList[matchedComment].like, 'this.commentList[matchedComment].like')
                this.updateId = null
            }).catch(e => alert(e))
        }
    }
}
</script>