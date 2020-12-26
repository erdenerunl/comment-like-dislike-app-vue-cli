<template>
  <div>
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
      <button
        type="button"
        class="btn btn-primary btn-sm ml-1"
        @click="addData"
      >
        Comment
      </button>
    </div>
  </div>
</template>

<script>
export default {
    props : ['commentData'],
    methods : {
        addData(){
            this.$emit('addComment', this.commentData)
        }
    }
};
</script>

<style>
</style>