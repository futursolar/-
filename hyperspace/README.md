hyperspace网页端节点自动重连脚本，本人提供想法，chatgpt撰写
下面复制到网页https://node.hyper.space/打开后，点击f12粘贴下面代码，粘贴不进去的话注意浏览器可能是让你输入允许并回车，输入后再试试能否粘贴并回车


(function(){
  // 使用 MutationObserver 监控整个页面的 DOM 变化
  const observer = new MutationObserver((mutationsList) => {
    for (let mutation of mutationsList) {
      mutation.addedNodes.forEach(node => {
        // 只对文本节点进行检查
        if (node.nodeType === Node.TEXT_NODE && node.textContent.includes("Disconnected")) {
          // 查找页面中包含 “Reconnect” 或 “重连” 文本的按钮
          const reconnectBtn = Array.from(document.querySelectorAll("button"))
            .find(b => b.innerText.includes("Disconnected") || b.innerText.includes("重连"));
          if (reconnectBtn) {
            console.log("检测到 'Disconnected' 状态，自动点击重连按钮。");
            reconnectBtn.click();
          }
        }
      });
    }
  });
  
  // 监听整个文档内的子节点变化（包括后代节点）
  observer.observe(document.body, {childList: true, subtree: true});
})();
