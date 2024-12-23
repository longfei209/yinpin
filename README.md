<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EasyMP3</title>
  <style>
    * {
      padding: 0;
      margin: 0;
    }

    .p10 {
      padding: 10px
    }

    .p20 {
      padding: 20px
    }

    .p30 {
      padding: 30px
    }

    .m10 {
      margin: 10px
    }

    .m20 {
      margin: 20px
    }

    .m30 {
      margin: 30px
    }

    .pl10 {
      padding-left: 10px
    }

    .pr10 {
      padding-right: 10px
    }

    .ml10 {
      margin-left: 10px
    }

    .mr10 {
      margin-right: 10px
    }

    .border1 {
      border: 1px solid;
    }

    .radius5 {
      border-radius: 5px;
    }

    .d-flex {
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .p-relative {
      position: relative;
    }

    .p-absolute {
      position: absolute;
    }

    .c-pointer {
      cursor: pointer;
    }

    .text-ellipsis {white-space: nowrap;text-overflow: ellipsis;overflow: hidden;}

    #app {
      height: 100vh;
      width: 100vw;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .box {
      font-size: 14px;
      width: 500px;
      height: 800px;
      border-radius: 10px;
      box-shadow: 5px 5px 10px 1px rgba(0, 0, 0, 0.5);
      display: flex;
      flex-direction: column;
      background: linear-gradient(180deg, lightblue, lightpink);
      color: darkcyan;
    }

    .version {
      top: 6px;
      left: 10px;
      font-size: 12px;
    }

    .title {
      top: 6px;
      left: 200px;
      font-size: 14px;
    }

    .playing-name {
      position: relative;
      top: 8px;
    }

    .how2use {
      right: 20px;
      bottom: 0;
      border: 1px solid;
      border-radius: 50%;
      width: 12px;
      height: 12px;
      font-size: 12px;
      line-height: 12px;
      text-align: center;
    }

    /* .player {
      height: 15%;
    } */

    .playlist {
      padding: 10px;
      height: 85%;
      overflow: auto;
      margin: 20px;
      background: #00000008;
      box-shadow: inset 1px 1px 2px 1px rgba(0, 0, 0, 0.3);
    }

    .playlist>li {
      list-style: none;
      font-size: 14px;
      height: 24px;
      line-height: 24px;
      border-radius: 5px;
    }

    .playlist>li:hover {
      cursor: pointer;
      box-shadow: 0px 0px 3px 0px rgba(0, 0, 0, 0.5);
    }

    .playlist>li.is-active {
      color: blueviolet;
      font-weight: 700;
    }

    audio {
      width: 100%;
    }

    audio::-webkit-media-controls-enclosure {
      background: transparent;
    }

    /* 时间戳 */
    audio::-webkit-media-controls-current-time-display,
    audio::-webkit-media-controls-time-remaining-display,
    audio::-webkit-media-controls-timeline {
      /* color: lightcoral; */
    }

    input[pseudo="-webkit-media-controls-timeline" i]::-internal-track-segment-background {
      /* color: lightcoral; */
    }

    /* 播放 */
    audio::-webkit-media-controls-play-button {
      display: none;
    }

    /* 声音控制 */
    audio::-webkit-media-controls-volume-control-container {
      /* display: none; */
    }

    /* 设置滚动条的宽度、高度、背景色和边框样式 */
    ::-webkit-scrollbar {
      width: 8px;
      background-color: #008b8b88;
      border-radius: 5px;
    }

    /* 设置滚动条滑块的背景色和圆角 */
    ::-webkit-scrollbar-thumb {
      background-color: #008b8b88;
      border-radius: 5px;
    }

    /* 设置滚动条滑块在悬停状态下的背景色和圆角 */

    ::-webkit-scrollbar-thumb:hover {
      background-color: darkcyan;
      border-radius: 5px;

    }

    /* 设置滚动条轨道的背景色和圆角 */

    ::-webkit-scrollbar-track {
      background-color: #f5f5f588;
      border-radius: 5px;
    }

    /* 设置滚动条轨道在悬停状态下的背景色和圆角 */

    ::-webkit-scrollbar-track:hover {
      background-color: #f5f5f599;
    }

    .flash {
      animation: flash 3s infinite;
    }

    @keyframes flash {
      0% {
        opacity: 0;
      }

      50% {
        opacity: 1;
      }

      80% {
        opacity: 1;
      }

      100% {
        opacity: 0;
      }
    }

    .btn {
      display: inline-block;
      text-align: center;
      padding: 4px 8px;
      border: none;
      border-radius: 5px;
      font-size: 12px;
      font-weight: bold;
      color: #fff;
      background: #2980b9;
      box-shadow: 0px 4px 0px #1d6b91;
      transition: all 0.1s ease-in-out;
      font-family: cursive;
      margin: 0 20px;
      width: 24px;
    }

    .btn:hover {
      background: #236ea0;
      box-shadow: 0px 4px 0px #185879;
      cursor: pointer;
    }

    .btn:active {
      background: #2c3e50;
      box-shadow: 0px 4px 0px #1a2533;
    }

    .btn-play {
      font-size: 14px;
      width: 30px;
      height: 24px;
      line-height: 24px;
    }
  </style>
</head>

<body>
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

  <div id="app">
    <div class="box">
      <div class="player p30 p-relative">
        <span class="version p-absolute">Ver 1.0</span>
        <span class="title p-absolute">EasyMP3播放器</span>
        <div class="ml10 mr10 flash playing-name">{{music?.name}}</div>
        <audio id="audio" :src="music?.url" autoplay controls @ended="next"></audio>
        <div class="d-flex">
          <span class="btn" @click="prev">{{btn.prev}}</span>
          <span class="btn btn-play" @click="playPause">{{isPlaying ? btn.pause : btn.play}}</span>
          <span class="btn" @click="next">{{btn.next}}</span>
        </div>
        <span class="how2use p-absolute c-pointer" @click="how2use">?</span>
      </div>
      <ul class="playlist radius5">
        <li class="pl10 text-ellipsis" :class="{'is-active': checkActive(item)}" v-for="(item, index) in playlist" :key="index"
          @click="changeSong(item, index)">{{index +
          1}}.{{item.name}}</li>
      </ul>
    </div>
  </div>

