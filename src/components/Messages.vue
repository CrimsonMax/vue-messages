<template>
  <div class="wrapper" v-on:scroll="pagination">
    <div class="messages">
      <div v-for="message in messages" :key="message.date" class="post">
        <div class="post-header">
          <span>{{
            new Date(message.date).toLocaleString("ru", {
              year: "numeric",
              month: "long",
              day: "numeric",
              timezone: "UTC",
            })
          }}</span>
          / <span style="font-weight: bold">{{ message.authorName }}</span> /
          <a href="{{message.authorUrl}}">{{ message.authorUrl }}</a>
        </div>
        <div class="post-text">
          {{ message.content }}
        </div>
        <div class="post-line"></div>
      </div>
      <div class="lds-roller" v-show="!loader">
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <div></div>
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
      loader: false,
    };
  },
  async beforeMount() {
    try {
      const info = await axios.get(
        `http://localhost:3000/messages?_limit=${this.num}`
      );
      this.messages = info.data;
    } catch (e) {
      console.log(e);
    }
  },
  methods: {
    pagination: function () {
      if (
        document.querySelector(".wrapper").scrollTop +
          document.querySelector(".wrapper").offsetHeight ===
        document.querySelector(".wrapper").scrollHeight
      ) {
        this.loader = true;
        this.num += 10;
        axios
          .get(`http://localhost:3000/messages?_limit=${this.num}`)
          .then((res) => (this.messages = res.data));
        setTimeout(() => {
          this.loader = false;
        }, 1000);
      }
    },
  },
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
  /* display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center; */
}

.messages {
  height: 100%;
  display: flex;
  flex-direction: column;
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

/*===================
  Loader
===================*/

.lds-roller {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
  margin: 0 auto;
  align-self: center;
}
.lds-roller div {
  animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 40px 40px;
}
.lds-roller div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: rgb(165, 16, 16);
  margin: -4px 0 0 -4px;
}
.lds-roller div:nth-child(1) {
  animation-delay: -0.036s;
}
.lds-roller div:nth-child(1):after {
  top: 63px;
  left: 63px;
}
.lds-roller div:nth-child(2) {
  animation-delay: -0.072s;
}
.lds-roller div:nth-child(2):after {
  top: 68px;
  left: 56px;
}
.lds-roller div:nth-child(3) {
  animation-delay: -0.108s;
}
.lds-roller div:nth-child(3):after {
  top: 71px;
  left: 48px;
}
.lds-roller div:nth-child(4) {
  animation-delay: -0.144s;
}
.lds-roller div:nth-child(4):after {
  top: 72px;
  left: 40px;
}
.lds-roller div:nth-child(5) {
  animation-delay: -0.18s;
}
.lds-roller div:nth-child(5):after {
  top: 71px;
  left: 32px;
}
.lds-roller div:nth-child(6) {
  animation-delay: -0.216s;
}
.lds-roller div:nth-child(6):after {
  top: 68px;
  left: 24px;
}
.lds-roller div:nth-child(7) {
  animation-delay: -0.252s;
}
.lds-roller div:nth-child(7):after {
  top: 63px;
  left: 17px;
}
.lds-roller div:nth-child(8) {
  animation-delay: -0.288s;
}
.lds-roller div:nth-child(8):after {
  top: 56px;
  left: 12px;
}
@keyframes lds-roller {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>