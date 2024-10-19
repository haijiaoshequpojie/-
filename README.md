// ==UserScript==
    // @name 海角社区破解版
    // @homepage https://hj588.top
    // @version 3.3.8
    // @description 🔥免费看付费视频 下载视频，海角社区破解版获取地址:hj588.top
    // @icon https://cdn.hj588.top/image/hao.png
    // @namespace 海角社区
    // @author jsxl
    // @include *://hj*.*/*
    // @include *://*.hj*.*/*
    // @include *://*.hai*.*/*
    // @include *://hai*.*/*
    // @include *://hj*/*
    // @include *://*.hj*/*
    // @include         
    // @include         
    // @include */post/details/*
    // @include *://blog.luckly-mjw.cn/*
    // @include *://tools.thatwind.com/*
    // @include *://tools.bugscaner.com/*
    // @match *://*/post/details*
    // @require https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js
    // @require https://cdnjs.cloudflare.com/ajax/libs/hls.js/1.5.8/hls.min.js
    // @require https://cdnjs.cloudflare.com/ajax/libs/dplayer/1.27.1/DPlayer.min.js
    // @run-at document-start
    // @grant unsafeWindow
    // @grant GM_addStyle
    // @grant GM_getValue
    // @grant GM_setValue
    // @grant GM_getResourceText
    // @grant GM_xmlhttpRequest
    // @charset UTF-8
    // @antifeature payment
    // @license MIT
// @downloadURL https://update.greasyfork.org/scripts/513140/%E2%8F%B3%E6%B5%B7%E8%A7%92%E7%A4%BE%E5%8C%BA%E7%A0%B4%E8%A7%A3%E2%8F%B3.user.js
// @updateURL https://update.greasyfork.org/scripts/513140/%E2%8F%B3%E6%B5%B7%E8%A7%92%E7%A4%BE%E5%8C%BA%E7%A0%B4%E8%A7%A3%E2%8F%B3.meta.js
    // ==/UserScript==
     
    var targetNode = document.documentElement;
    var config = { attributes: true, childList: true, subtree: true };
     
    var observer = new MutationObserver(function(mutationsList, observer) {
        mutationsList.forEach(function(mutation) {
     
            if (mutation.target.tagName !== 'TITLE') {
              var divElement = document.querySelector('div.nickname > span:first-child + span');
              if (divElement) {
                // 获取网址
                var currentURL = window.location.href;
                if (currentURL.includes("last")) {
                    var minititle = "最新帖子";
                } else if (currentURL.includes("essence")) {
                    var minititle = "精华帖子";
                } else if (currentURL.includes("reward")) {
                    var minititle = "悬赏帖子";
                } else if (currentURL.includes("sell")) {
                    var minititle = "出售帖子";
                } else {
                    var minititle = "全部帖子";
                }
                var nickname = divElement.previousElementSibling.textContent;
                var idInfo = divElement.textContent;
                document.title = nickname+"的"+ minititle + "-海角社区";
              }
              //______________________________________________________________
     
              //帖子的标题修改
              var relativeH2 = document.querySelector('h2 span');
              if (relativeH2) {
                var text = relativeH2.textContent;
                var parentElement = document.querySelector('span a.hjbox-linkcolor').parentNode;
                if (parentElement) {
                    var keyword = parentElement.textContent.trim();
                    document.title = text + "_" + keyword + "-海角社区";
                }
              }
              //______________________________________________________________
     
              //首页标题
              var liElements = document.querySelectorAll('li.menu-li.menu-item');
              var keywords = [];
              liElements.forEach(function(liElement) {
                  var linkElement = liElement.querySelector('a.menu-link');
     
                  if (linkElement && linkElement.classList.contains("visible")) {
                      var keyword = linkElement.querySelector("span:last-child").textContent;
                      keywords.push(keyword);
                  }
              });
     
              if (keywords.length > 0) {
                  document.title = keywords.join(", ") + "-海角社区";
     
     
                  var visibleKeywordElements = document.querySelectorAll('li div.child_link.lahjyu.visible');
                  var visibleKeywords = [];
                  visibleKeywordElements.forEach(function(visibleKeywordElement) {
                      var visibleKeyword = visibleKeywordElement.textContent.trim();
                      visibleKeywords.push(visibleKeyword);
                  });
                  if (visibleKeywords.length > 0) {
                      var cleanedValue = visibleKeywords.join(", ").replace(/\s*VIP\d*\s*/g, '');
                      document.title = keywords.join(", ") + "-" + cleanedValue + "-海角社区";
     
                      var activeTitle = document.querySelector('.active a');
                      if (activeTitle) {
                        var titleText = activeTitle.textContent.trim();
                        document.title = keywords.join(", ") + "-" + cleanedValue + "-" + titleText + "-海角社区";
                      }
                  }
     
                  var activeTitle = document.querySelector('.title.active');
                  if (activeTitle) {
                    var titleText = activeTitle.textContent.trim();
                    document.title = keywords.join(", ") + titleText + "-海角社区";
                  }
                }
              //______________________________________________________________
     
     
              //发帖时标题
              var hasDraft = document.querySelector('.draft') !== null;
              var hasSubmitBtn = document.querySelector('.common-submitBtn') !== null;
              var hasNotice = document.querySelector('span[style="font-size: 12px; color: rgb(255, 101, 101);"]') !== null;
     
              var result = "";
     
              if (hasDraft && hasSubmitBtn && hasNotice) {
                result = "发帖";
                document.title = result + "-海角社区";
              }
              //______________________________________________________________
     
     
     
            }
     
          var tidioChatDiv = document.getElementById("tidio-chat");
          if (tidioChatDiv) {
              tidioChatDiv.remove();
          }
     
        });
    });
     
    observer.observe(targetNode, config);
     
     
    var scriptName = 'mdui.min.js'; // 指定脚本文件名
    if (!hasScriptInSourceCode(scriptName)) {
      var cssLink = document.createElement('link');
      cssLink.rel = 'stylesheet';
     
      cssLink.href = 'https://unpkg.com/mdui@1.0.2/dist/css/mdui.min.css';
      var jsScript = document.createElement('script');
      jsScript.src = 'https://unpkg.com/mdui@1.0.2/dist/js/mdui.min.js';
     
      document.head.appendChild(cssLink);
      document.head.appendChild(jsScript);
    }
    // 判断网页源代码是否包含指定的脚本文件
    function hasScriptInSourceCode(scriptName) {
      var sourceCode = document.documentElement.innerHTML;
      return sourceCode.includes(scriptName);
    }
     
     
    // 创建按钮元素
    var buttonElement = document.createElement('button');
    buttonElement.className = 'mdui-fab mdui-fab-fixed mdui-ripple mdui-color-pink';
    var iconElement = document.createElement('i');
    iconElement.className = 'mdui-icon material-icons';
    iconElement.textContent = 'arrow_upward';
    buttonElement.appendChild(iconElement);
    var body = document.body;
    body.appendChild(buttonElement);
    // 添加按钮点击事件
    buttonElement.addEventListener('click', function() {
        window.scrollTo({ top: 0, behavior: 'smooth' });
    });
     
    function findTargetElement(targetContainer, maxTryTime = 30){
     const body = window.document;
     let tabContainer;
     let tryTime = 0;
     let startTimestamp;
     return new Promise((resolve, reject) => {
      function tryFindElement(timestamp) {
       if (!startTimestamp) {
        startTimestamp = timestamp;
       }
       const elapsedTime = timestamp - startTimestamp;
       if (elapsedTime >= 500) {
        console.log("find element：" + targetContainer + "，this" + tryTime + "num")
        tabContainer = body.querySelector(targetContainer)
        if (tabContainer) {
         resolve(tabContainer)
        } else if (++tryTime === maxTryTime) {
         reject()
        } else {
         startTimestamp = timestamp
        }
       }
       if (!tabContainer && tryTime < maxTryTime) {
        requestAnimationFrame(tryFindElement);
       }
      }
      requestAnimationFrame(tryFindElement);
     });
    }
     
    function shiowTips(){
     GM_addStyle(`
      #my-mask{
       position: fixed;
       top:0;
       left:0;
       right:0;
       bottom:0;
       background-color: #0000004d;
       z-index: 999999;
      }
      #my-container{
       position: absolute;
       top: 50%;
       left: 50%;
       transform: translate(-50%, -50%);
       width: 70%;
       border-radius: 15px;
       background-color: white;
       padding: 10px 15px;
       z-index: 999998;
      }
      #my-container .title{
       display: block;
       font-size: 20px;
       color: #222;
       font-weight: 500;
       text-align: center;
       margin: 10px 0;
      }
      #my-container .content{
       color: #6a6a6a;
       letter-spacing: 2px;
       font-size: 15px;
       line-height: 22px;
      }
      #my-container .btn{
       display: block;
      }
      #my-container .btn boutton{
       display: block;
       margin: 10px auto;
       margin-top: 30px;
       width: 82px;
       height: 35px;
       border-radius: 30px;
       border: none;
       color: white;
       transition: all 0.3s ease;
       background-color: #ec407a;
       line-height: 35px;
       text-align: center;
      }
     `)
     findTargetElement('body').then(res =>{
      $(res).append(`
       <div id="my-mask">
        <div id="my-container">
         <view class="title">公告</view>
         <view class="content">
          抱歉，此脚本为付费脚本，请通过链接<a href="https://hj588.top/" style="color: #e91e63;text-decoration: underline;">https://hj588.top/</a>购买后安装最新版本脚本再使用，谢谢!
         </view>
         <view class="btn">
          <boutton>去购买</boutton>
         </view>
        </div>
       </div>
      `)
      $("#my-container .btn").on('click', ()=>{
       location.href = "https://hj588.top/"
      })
     })
    }
    if(!location.href.includes('hj588.top')){
     shiowTips()
    }
