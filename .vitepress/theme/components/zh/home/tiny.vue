<!--
SPDX-FileCopyrightText: 2023 UnionTech Software Technology Co., Ltd.

SPDX-License-Identifier: LGPL-3.0-or-later
-->

<template>
  <TinyLayout class="tiny-layout">
    <template #header>
      <div>
        <TinyHeader :expand="expand" @change="tinyHeaderChange" />
      </div>
    </template>
    <template #content>
      <div class="banner">
        <div class="w-center">
          <div class="enter">
            <h1>玲珑，为兼容与安全而生</h1>
            <p class="describe">
              玲珑是一种新型的独立包管理工具集，致力于治理Linux系统下传统软件包格式复杂、交叉的依赖关系导致的各种兼容性问题，以及过于松散的权限管控导致的安全风险。
            </p>
            <div class="link-wrap">
              <a href="javascript:void(0);" @click="jump('/guide/ll-builder/introduction.html')" class="link quick">10分钟快速构建</a>
              <a href="javascript:void(0);" @click="jump('/guide/ll-builder/manifests.html#runtime-20-5-0-包含依赖项')" class="link plain ml-15">Runtime清单</a>
              <a href="https://bbs.deepin.org" target="_blank" class="link plain ml-15">社区讨论</a>
            </div>
          </div>
        </div>
      </div>
      <!-- block1 (玲珑意味着什么？) -->
      <div class="mean-block ">
        <div class="w-center block">
          <div class="title">
            <span>玲珑意味着什么？</span>
          </div>
          <div>
            <div class="to w-center to-user">
              <h2>对用户来说</h2>
              <h3><i class="selected"></i>更稳定</h3>
              <p>大大减少了系统升级应用起不来，体验了一款新的应用导致系统损坏等情况。</p>
              <h3><i class="selected"></i>更安全</h3>
              <p>拒绝应用未授权读取用户数据，不小心安装了恶意应用也不会入侵系统。</p>
              <h3><i class="selected"></i>更易用</h3>
              <p>无需安装双击即可运行，删除文件即可卸载应用。</p>
            </div>
            <div class="to w-center to-dev">
              <h2>对开发者来说</h2>
              <h3><i class="selected"></i>更独立</h3>
              <p>应用与系统相互隔离，无需过多关注系统环境变化，支持多发行版内容也变得容易。</p>
              <h3><i class="selected"></i>更兼容</h3>
              <p>避免依赖冲突，多版本共存，应用兼容性更易保证。</p>
              <h3><i class="selected"></i>易分发</h3>
              <p>在线分发与离线分发均支持，可加入发行版生态，也可在自己的渠道进行分发。</p>
            </div>
          </div>
        </div>
      </div>
      <!-- block2 (玲珑的五大特性) -->
      <div class="feature-block">
        <div class="w-center block">
          <div class="title">
            <span>玲珑的五大特性</span>
          </div>
          <div class="w-center" style="padding: 0px 15px;">
            <div class="card">
              <i class="f-icon f1"></i>
              <h3>发行版已集成</h3>
              <p>deepin 正式集成玲珑，提供美观便捷的图形化管理。</p>
            </div>
            <div class="card">
              <i class="f-icon f2"></i>
              <h3>启动速度快</h3>
              <p>提供机制供发行版针对runtime进行深度优化，减小体积提升。</p>
            </div>
            <div class="card">
              <i class="f-icon f3"></i>
              <h3>兼容性强</h3>
              <p>独立的runtime使得应用与系统隔离，增强兼容性。</p>
            </div>
            <div class="card">
              <i class="f-icon f4"></i>
              <h3>安全性高</h3>
              <p>容器化技术与权限控制机制，提升安全性。</p>
            </div>
            <div class="card">
              <i class="f-icon f5"></i>
              <h3>易于分发</h3>
              <p>在线与离线分发均支持，无需安装即可运行。</p>
            </div>
          </div>
        </div>
      </div>
      <!-- block3 (玲珑不断丰富的生态) -->
      <div class="app-block">
        <div class="w-center block">
          <div class="title">
            <span>玲珑不断丰富的生态</span>
          </div>
          <div class="u-flex u-items-center u-justify-center">
            <ul class="app-list">
              <li v-for="app of apps" :key="app.key">
                <div class="card u-flex u-items-center u-justify-start">
                  <i :style="{backgroundImage:app.icon}"></i>
                  <span>{{app.text}}</span>
                </div>
              </li>
            </ul>
          </div>
          <div class="go-stroe">
            <a href="https://store.linglong.dev" target="_blank">进入玲珑商店 -></a>
          </div>
        </div>
      </div>
      <!-- block4 (体验离线bundle格式) -->
      <div class="bundle-block">
        <div class="w-center block">
          <div class="title">
            <span>体验离线bundle格式</span>
            <p class="sub">可在Deepin、Ubuntu和Debian上体验离线bundle格式，无需安装即可运行，更多发行版持续支持中…</p>
          </div>
          <div class="card" v-for="bundle of bundles" :key="bundle.appId">
            <i class="app" :style="{backgroundImage:bundle.icon}"></i>
            <div class="app-name u-truncate">{{bundle.name}}</div>
            <a :href="bundle.downloadUrl">
              <i class="down"></i>
              下载体验
            </a>
          </div>
        </div>
      </div>
    </template>
    <template #footer>
      <TinyFooter />
    </template>
  </TinyLayout>
  <div v-if="expand" @click="hideMask" class="mask"></div>
</template>
<script setup>
import FullLayout from '../../layout/full.vue'
import TinyLayout from '../../layout/tiny.vue'
import Header from '../header/index.vue'
import TinyHeader from '../header/tiny-header.vue'
import Footer from '../footer/index.vue'
import TinyFooter from '../footer/tiny-footer.vue'

import { ref } from "@vue/reactivity"

const apps = ref([
  { key: 1, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/com.deepin.gomoku.svg)', text: '五子棋' },
  { key: 2, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/com.deepin.lianliankan.svg)', text: '连连看' },
  { key: 3, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/dde-calendar.svg)', text: '日历' },
  { key: 4, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-calculator.svg)', text: '计算器' },
  { key: 5, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-editor.svg)', text: '文本编辑器' },
  { key: 6, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-reader.svg)', text: '文档查看器' },
  { key: 7, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-compressor.svg)', text: '归档管理器' },
  { key: 8, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/org.deepin.browser.svg)', text: '浏览器' },
  { key: 9, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-mail.svg)', text: '邮箱' },
  { key: 10, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-album.svg)', text: '相册' },
  { key: 11, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-draw.svg)', text: '画板' },
  { key: 12, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-image-viewer.svg)', text: '看图' },
  { key: 13, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-camera.svg)', text: '相机' },
  { key: 14, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-music.svg)', text: '音乐' },
  // { key: 15, icon: 'url(https://mirror-repo-linglong.deepin.com/icon/deepin-movie.svg)', text: '影院' }
])
const bundles = [{
  appId: "com.163.music",
  arch: "x86_64",
  description: "网易云音乐是一款专注于发现与分享的音乐产品，依托专业音乐人、DJ、好友推荐及社交功能，在线音乐服务主打歌单、社交、大牌推荐和音乐指纹，以歌单、DJ节目、社交、地理位置为核心要素，主打发现和分享。",
  icon: "url(https://store.chinauos.com/api/public/blob/1dda7a14-738e-4ce4-b81a-6d6ba0d3c3f6)",
  id: 0,
  name: "网易云音乐",
  version: "1.2.1.1",
  downloadUrl: "https://mirror-repo-linglong.deepin.com/bundle/com.163.music_1.2.1.1_x86_64.uab"
}, {
  appId: "cn.wps.wps-office",
  arch: "x86_64",
  "description": "WPS Office 2019 for Linux 办公软件，是一款兼容、开放、高效、安全并极具中文本土化优势的办公软件。支持国内外主流软硬件系统，其专业的图文混排功能、强有力的计算引擎和强大的数据处理功能、丰富的动画效果设置、公文处理等，可以充分满足国内外用户在Linux体系下高效办公的要求。\nWPS Office 2019 for Linux在文字排版、表格计算、演示动画三大核心功能上做到底层兼容，可以直接创建、读取、编辑、保存如doc、xls、ppt、pps等格式的文档、国际标准OOXML文档（如docx、xlsx、pptx、ppsx等格式的文档）。\n客服热线：400-822-9012\nQQ群：858835097\n微信客服：搜索 \"WPS客户服务\"",
  icon: "url(https://store.chinauos.com/api/public/blob/ec4435df-037e-40cf-8417-67993b89dd0e)",
  name: "WPS2019 社区版",
  version: "11.1.0.11664",
  downloadUrl: "https://mirror-repo-linglong.deepin.com/bundle/cn.wps.wps-office_11.1.0.11664_x86-64.uab"
}, {
  appId: "com.baidu.baidunetdisk",
  arch: "x86_64",
  description: "百度网盘为百度旗下的一款云存储产品，用户可以轻松将自己的文件上传到网盘上，并可跨终端随时随地查看和分享。",
  icon: "url(https://store.chinauos.com/api/public/blob/5bb10bee-53de-4ed0-ac65-8374c8c3e8f4)",
  name: "百度网盘",
  version: "4.3.0",
  downloadUrl: "https://mirror-repo-linglong.deepin.com/bundle/com.baidu.baidunetdisk_4.3.0_x86_64.uab"
}, {
  appId: "com.xunlei.download",
  arch: "x86_64",
  description: "十八年技术沉淀，专注下载传输，成就用户信赖的必备工具”，迅雷团队首次推出 linux 界面版本，为国产芯片和国产操作系统助力，为用户提供极速，流畅，便捷的下载服务。\n\n【支持国芯、支持国产操作系统】\n\n       支持多种芯片，适配龙芯，适配国产操作系统。\n\n【一样下载体验】\n\n       一样强大而稳定的下载内核，简洁的操作界面，一样的下载速度，一样的下载信息呈现。\n\n【简约的界面交互】 　　\n\n       简约设计，精致的简约体验；linux 迅雷界面尺寸更加小巧，小屏幕也能适应。　\n\n【强大的软件框架】\n\n       linux 迅雷使用基于 “Electron” 的软件框架，使界面响应将更加流畅，文字显示效果更加清晰细腻。\n\n",
  icon: "url(https://store.chinauos.com/api/public/blob/5266244f-5df0-4512-ac0e-b980eba060f6)",
  name: "迅雷",
  version: "1.0.0.2",
  downloadUrl: "https://mirror-repo-linglong.deepin.com/bundle/com.xunlei.download_1.0.0.2_x86_64.uab"
}]

const expand = ref(false)
const tinyHeaderChange = (isExpand) => {
  expand.value = isExpand
}
const hideMask = () => {
  expand.value = false
}
const jump = (url) => {
  location.href = url
}
</script>

<style lang="scss" scoped>
@media screen and (min-width: 1200px) {
  .full-layout {
    display: block;
  }
  .tiny-layout {
    display: none;
  }
}
.w-center {
  margin: auto;
}
.block {
  padding: 40px 0px;
  .title {
    margin: auto;
    line-height: 1;
    font-size: 20px;
    font-weight: 500;
    color: #0a1943;
    margin-bottom: 24px;
    text-align: center;
    .sub {
      margin-top: 24px;
      font-size: 14px;
      font-weight: 400;
      padding: 0px 24px;
      color: rgba(0, 0, 0, 0.65);
      line-height: 1.5;
    }
  }
}
.banner {
  width: 100%;
  height: 468px;
  padding: 30px;
  background-image: url(/asset/home/tiny/banner.png);
  background-size: cover;
  background-color: #0e1016;
  background-repeat: no-repeat;
  background-position: bottom;
  .enter {
    color: #ffffff;
    margin-top: 45px;
    h1 {
      text-align: center;
      font-size: 24px;
      font-weight: 500;
      margin-bottom: 24px;
    }
    .describe {
      font-size: 14px;
      font-weight: 400;
      line-height: 26px;
    }
  }

  .link-wrap {
    text-align: center;
    margin-top: 30px;
    .link {
      display: inline-block;
      color: #3266fb;
      outline: none;
      text-decoration: none;
      border-radius: 8px;
      padding: 5px 12px;
      font-size: 12px;
      font-weight: 500;
      text-align: center;
      cursor: pointer;
    }
    .quick {
      background-color: #025bff;
      color: #ffffff;
      &:hover {
        background-color: #3179ff;
      }
    }
    .plain {
      background-color: #ffffff;
      &:hover {
        color: #0a1943;
      }
    }
    .ml-15 {
      margin-left: 12px;
    }
  }
}
.mean-block {
  padding: 0px 15px;
  background-color: #ffffff;
  .to {
    background-color: #f9f9f9;
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    padding: 24px 20px;
    background-repeat: no-repeat;
    background-position: right bottom;
    background-size: 290px 304px;
    h2 {
      font-size: 18px;
      font-weight: 500;
      color: #0a1943;
      margin-bottom: 24px;
    }
    h3 {
      font-size: 16px;
      font-weight: 500;
      color: #0a1943;
      margin-top: 30px;
      margin-bottom: 15px;
      .selected {
        vertical-align: middle;
        display: inline-block;
        width: 20px;
        height: 20px;
        background: url(/asset/home/selected.svg) no-repeat 50% / cover;
        margin-right: 4px;
      }
    }
    p {
      font-size: 14px;
      font-weight: 400;
      color: rgba(0, 0, 0, 0.65);
      padding-left: 25px;
    }
  }
  .to-user {
    background-image: url(/asset/home/user-bg.png);
  }
  .to-dev {
    margin-top: 24px;
    background-image: url(/asset/home/dev-bg.png);
  }
}
.feature-block {
  background: #eef1f7 url(/asset/home/tiny/feature-bg.png) no-repeat 100% / cover;
  .card {
    padding: 30px;
    height: 180px;
    background-color: #ffffff;
    margin-bottom: 15px;
    border-radius: 8px;
    &:last-child {
      margin-bottom: 0px;
    }
    .f-icon {
      display: block;
      width: 48px;
      height: 48px;
      background-position: center;
      background-repeat: no-repeat;
      background-size: contain;
    }
    .f1 {
      background-image: url(/asset/home/f1.png);
    }
    .f2 {
      background-image: url(/asset/home/f2.png);
    }
    .f3 {
      background-image: url(/asset/home/f3.png);
    }
    .f4 {
      background-image: url(/asset/home/f4.png);
    }
    .f5 {
      background-image: url(/asset/home/f5.png);
    }
    h3 {
      font-size: 16px;
      font-weight: 500;
      line-height: 1;
      color: #0a1943;
      margin: 24px 0px 8px;
    }
    p {
      font-size: 14px;
      font-weight: 400;
      color: rgba(0, 0, 0, 0.65);
    }
  }
}
.app-block {
  background-color: #ffffff;
  .app-list {
    overflow: hidden;
    list-style: none;
    padding: 0px 15px !important;
    border-radius: 8px;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    width: 100%;
    li {
      position: relative;
      text-align: center;
      color: #606266;
      height: 72px;
      font-size: 16px;
      transition: background-color 0.3s;
      .card {
        height: 60px;
        padding: 16px;
        border: 1px solid #ececec;
        border-radius: 8px;
        i {
          display: block;
          width: 40px;
          height: 40px;
          background-position: center;
          background-repeat: no-repeat;
          background-size: contain;
        }
        span {
          font-size: 16px;
          font-weight: 500;
          margin-left: 8px;
        }
      }
      &:nth-child(2n + 1) {
        .card {
          margin-right: 6px;
        }
      }
      &:nth-child(2n + 2) {
        .card {
          margin-left: 6px;
        }
      }
    }
  }
  .go-stroe {
    text-align: center;
    padding-top: 16px;
    a {
      outline: none;
      text-decoration: none;
      color: #003296;
      font-size: 16px;
      font-weight: 500;
      &:hover {
        color: rgba(0, 50, 150, 0.7);
      }
    }
  }
}
.bundle-block {
  padding: 0px 15px;
  background-color: #fafafc;
  .card {
    background-color: #ffffff;
    border-radius: 8px;
    padding: 24px 20px 32px;
    text-align: center;
    margin-bottom: 15px;
    &:last-child {
      margin-bottom: 0px;
    }
    &:hover {
      box-shadow: 0px 6px 20px 0px rgba(0, 0, 0, 0.1);
    }
    i.app {
      margin: auto;
      display: block;
      width: 64px;
      height: 64px;
      background-position: center;
      background-repeat: no-repeat;
      background-size: contain;
    }
    .app-name {
      font-size: 16px;
      font-weight: 500;
      color: #0a1943;
      margin-top: 16px;
      margin-bottom: 32px;
    }
    a {
      display: block;
      padding: 7px 18px;
      width: 125px;
      margin: auto;
      font-size: 16px;
      font-weight: 400;
      border: 1px solid rgba(0, 50, 150, 0.5);
      border-radius: 8px;
      color: #003296;
      &:hover {
        color: rgba(0, 50, 150, 0.7);
        border: 1px solid #003296;
      }
      .down {
        display: inline-block;
        vertical-align: middle;
        margin-bottom: 3px;
        width: 16px;
        height: 16px;
        background-position: center;
        background-repeat: no-repeat;
        background-size: contain;
        background-image: url(/asset/home/download.svg);
      }
    }
  }
}
.mask {
  position: fixed;
  left: 0px;
  bottom: 0px;
  width: 100%;
  height: calc(100vh - 183px);
  background-color: rgba($color: #333, $alpha: 0.5) !important;
}
</style>