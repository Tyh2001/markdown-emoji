<script lang="ts" setup>
import { emoji } from './json/emoji.json'
import Clipboard from 'clipboard'
import 'tyh-ui2/style/index.css'
import { Message } from 'tyh-ui2'

const copyCode = (node: string): void => {
  new Clipboard(node)
  Message({ message: '复制成功', type: 'primary', round: true })
}
</script>

<template>
  <h1 class="title">Markdown Emoji</h1>

  <ul class="list">
    <li v-for="(item, key, index) in emoji" :key="index" class="item">
      <div class="num">{{ index + 1 }}</div>

      <div class="emoji">{{ item }}</div>

      <div class="option">
        <div class="left" :data-clipboard-text="`:${key}:`" @click="copyCode('.left')">复制代码</div>
        <div class="right" :data-clipboard-text="item" @click="copyCode('.right')">复制表情</div>
      </div>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0
}

.title {
  text-align: center;
  color: #333;
}

.list {
  display: flex;
  flex-wrap: wrap;

  .item {
    position: relative;
    list-style: none;
    width: 140px;
    height: 140px;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    border: 1px solid #eee;

    .num {
      position: absolute;
      top: 3px;
      left: 3px;
      font-size: 12px;
      color: rgb(207, 207, 207);
    }

    .emoji {
      font-size: 30px;
      cursor: default;
    }

    &:hover {
      .option {
        transition: .6s;
        opacity: 1;
      }
    }

    .option {
      display: flex;
      align-items: center;
      width: 100%;
      position: absolute;
      bottom: 0;
      opacity: 0;

      .left,
      .right {
        width: 50%;
        font-size: 14px;
        display: inline-flex;
        justify-content: center;
        align-items: center;
        height: 30px;
        cursor: pointer;

        &:hover {
          transition: .4s;
          background: #eee;
          color: #2d5af1;
        }
      }
    }
  }
}
</style>
