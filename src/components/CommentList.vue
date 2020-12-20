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
              <button type="button" class="btn btn-success btn-sm mr-1" @click="isLike(comment.id)">Like {{ likeCounter }} </button>
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
            likeCounter : 0,
            dislikeCounter : 0
        }
    },
    methods : {
        isLike(id){
            axios.patch(`http://localhost:3000/comments/${id}`).then((response) => {
                response.data.like++
                
                console.log(response.data.like)
            }).catch((e)=> {
                alert(e)
            })
            this.likeCounter++
        }
    }
}
</script>