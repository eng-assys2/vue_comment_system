<template>
  <div class="form-todo form-group">
    <p>
      <input
        placeholder="Author's Name"
        type="text"
        name="author"
        id="author"
        class="form-control"
        v-model="inputAuthor"
      />
    </p>
    <p>
      <textarea
        placeholder="Comment"
        name="message"
        id="message"
        cols="30"
        rows="10"
        class="form-control"
        v-model="inputMessage"
      ></textarea>
    </p>
    <button type="submit" class="btn btn-primary" v-on:click="addComment">Send</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputAuthor: "",
      inputMessage: ""
    };
  },
  methods: {
    addComment() {
      if (this.inputMessage.trim() === "") {
        alert("Message cannot be empty")
        return
      }

      this.$emit("add-todo", {
        name: this.inputAuthor,
        message: this.inputMessage
      }); // Propagate an event

      this.inputAuthor = ""
      this.inputMessage = ""
    }
  }
};
</script>


<style>
</style>