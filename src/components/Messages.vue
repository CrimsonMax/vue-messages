<template>
  <div class="wrapper">
    <div class="messages">
      <div v-for="message in messages" :key="message.date" class="post">
        <div class="post-header">
          <span>{{ message.date }}</span> /
          <span style="font-weight: bold">{{ message.authorName }}</span> /
          <a href="{{message.authorUrl}}">{{ message.authorUrl }}</a>
        </div>
        <div class="post-text">
          {{ message.content }}
        </div>
        <div class="post-line"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      messages: [],
      num: 10,
    };
  },
  async created() {
    try {
      const info = await axios.get(
        `http://localhost:3000/messages?_limit=${this.num}`
      );
      this.messages = info.data;
    } catch (e) {
      console.log(e);
    }
  },
  // methods: {
    // v-on:scroll="pagination"
  //   pagination: function () {
  //     console.log("scrollTop", document.querySelector(".wrapper").scrollTop);
  //     console.log(
  //       "scrollHeight",
  //       document.querySelector(".wrapper").scrollHeight
  //     );
  //     if (
  //       document.querySelector(".wrapper").scrollTop +
  //         document.querySelector(".wrapper").offsetHeight ===
  //       document.querySelector(".wrapper").scrollHeight
  //     ) {
  //       this.num += 10;
  //       debugger;
  //       console.log(this.num);
  //       const NewInfo = axios.get(
  //         `http://localhost:3000/messages?_limit=${this.num}`
  //       );
  //       this.messages = NewInfo.data;
  //     }
  //   },
  // },
};
</script>

<style scoped>
.wrapper {
  width: 800px;
  height: 400px;
  margin: 1rem auto;
  box-shadow: 4px 4px 8px 0px rgb(34 60 80 / 40%);
  overflow-y: scroll;
  background-color: floralwhite;
}

.messages {
  height: 100%;
}

.post {
  width: 90%;
  padding: 0.5em;
}

.post-text {
  margin: 1em 0;
}

.post-line {
  border-bottom: 2px solid gray;
  margin-bottom: 1em;
}

/*===================
  Styled scrollbar
===================*/

::-webkit-scrollbar-button {
  background-image: url("");
  background-repeat: no-repeat;
  width: 5px;
  height: 0px;
}

::-webkit-scrollbar-track {
  background-color: #ecedee;
}

::-webkit-scrollbar-thumb {
  -webkit-border-radius: 0px;
  border-radius: 0px;
  background-color: black;
}

::-webkit-scrollbar-thumb:hover {
  background-color: black;
}

::-webkit-resizer {
  background-image: url("");
  background-repeat: no-repeat;
  width: 4px;
  height: 0px;
}

::-webkit-scrollbar {
  width: 4px;
}
</style>