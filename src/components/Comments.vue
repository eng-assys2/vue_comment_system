<template>
  <div class="container">
    <h1>Comments</h1>
    <hr />

    <FormTodo v-on:add-todo="addComment" />

    <div class="list-group">
      <p v-if="comments.length == 0">No comments are here yet ...</p>
      <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
        <span class="comment__author">
          Author:
          <strong>{{ comment.name }}</strong>
        </span>
        <p>{{ comment.message }}</p>
        <div>
          <a v-on:click.prevent="removeComment(index)" href="#" title="Remove">Remove</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import FormTodo from "./FormTodo";

export default {
  // por baixo o compilador do Vue instancia esse objeto e da um new Vue
  components: {
    FormTodo
  },
  data() {
    return {
      comments: [
        {
          name: "Lucas",
          message: "Comment 1"
        },
        {
          name: "Vinícius",
          message: "Comment 2"
        }
      ]
    };
  },
  methods: {
    addComment(comment) {
      this.comments.push(comment);
    },
    removeComment(commentIndex) {
      this.comments.splice(commentIndex, 1);
    }
  },
  computed: {
    // propriedade cacheada, só é executada em casos de mudanças
    allComments() {
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anônimo" : comment.name
      }));
    }
  },
  watch: {
    // comments(val) {
    //   // qualquer alteração dentro de comentários vai chamar essa função
    //   console.log(JSON.stringify(val))
    // }
  }
};
</script>


<style lang="stylus" scoped></style>