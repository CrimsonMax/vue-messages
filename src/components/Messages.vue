<template>
  <div class="wrapper">
    <div class="messages">
      <div class="post">
        <div class="post-header">
          <span>03:55, 1 сентября 1986г.</span> /
          <span style="font-weight: bold">Успенский</span> /
          <a href="http://happy-kids.ru">http://happy-kids.ru</a>
        </div>
        <div class="post-text">
          Я был когда-то странной\nИгрушкой безымянной,\nК которой в
          магазине\nНикто не подойдет.\nТеперь я Чебурашка,\nМне каждая
          дворняжка\nПри встрече сразу\nЛапу подает!\n\nМне не везло сначала,\nИ
          даже так бывало:\nКо мне на день рожденья\nНикто не приходил.\nТеперь
          я вместе с Геной\nОн не обыкновенный,\nОн самый лучший\nВ мире
          крокодил!
        </div>
        <div class="post-line"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
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