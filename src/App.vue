<script lang="ts" setup>
  import { emoji } from './json/emoji.json'
  import Clipboard from 'clipboard'
  import { FMessage, FButton, FCard, FBackTop } from 'fighting-design'
  import 'fighting-design/theme/message.css'
  import 'fighting-design/theme/button.css'

  const copyCode = (node: string): void => {
    new Clipboard(node)
    FMessage({
      message: '复制成功',
      type: 'primary',
      round: true,
    })
  }
</script>

<template>
  <f-back-top>返回顶部</f-back-top>

  <f-card title="Markdown Emoji">
    <ul class="list">
      <li v-for="(item, key, index) in emoji" :key="index" class="item">
        <div class="emoji">{{ item }}</div>

        <div class="option">
          <f-button
            simple
            size="small"
            type="primary"
            :data-clipboard-text="`:${key}:`"
            @click="copyCode('.left')"
          >
            复制代码
          </f-button>
          <f-button
            simple
            size="small"
            type="success"
            :data-clipboard-text="item"
            @click="copyCode('.right')"
          >
            复制表情
          </f-button>
        </div>
      </li>
    </ul>
  </f-card>
</template>

<style lang="scss" scoped>
  * {
    margin: 0;
    padding: 0;
  }

  .list {
    display: flex;
    flex-wrap: wrap;
    margin: auto;

    .item {
      position: relative;
      list-style: none;
      width: 140px;
      height: 140px;
      display: inline-flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;

      .emoji {
        font-size: 30px;
        cursor: default;
      }

      &:hover {
        .option {
          transition: 0.6s;
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
      }
    }
  }
</style>
