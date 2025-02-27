# 抽人程序下载链接
[<button style="padding: 10px 20px; background-color: #4CAF50; color: white; border: none; border-radius: 5px;">点击下载</button>](https://www.123865.com/s/KypqVv-lnJzH)

<div id="chatbot" style="position:fixed;bottom:20px;right:20px;width:300px;background:#fff;box-shadow:0 0 15px rgba(0,0,0,0.1);border-radius:10px;">
  <div style="background:#007bff;color:white;padding:15px;border-radius:10px 10px 0 0;">
    <b>网站助手</b>
    <button onclick="document.getElementById('chatbot').remove()" style="float:right;background:none;border:none;color:white;">×</button>
  </div>
  <div id="chat-area" style="height:200px;overflow-y:auto;padding:10px;">
    <div class="bot-msg">你好！我是网站AI助手，可以问我：<br>• 网站功能<br>• 最新更新<br>• 联系信息</div>
  </div>
  <input type="text" id="user-input" placeholder="输入问题..." style="width:100%;padding:10px;border:none;border-top:1px solid #ddd;" 
         onkeypress="if(event.keyCode==13) handleInput(this.value)">
</div>

<script>
const responses = {
  "功能": "本站提供XXX服务，主要功能包括：<br>• 文件下载<br>• 技术博客<br>• 项目展示",
  "更新": "最近更新：<br>• 新增下载按钮（2024.3）<br>• 优化移动端显示",
  "联系": "联系方式：<br>📧 example@domain.com<br>📱 关注我们的Twitter @example"
};

function handleInput(text) {
  const chatArea = document.getElementById('chat-area');
  chatArea.innerHTML += `<div class="user-msg" style="text-align:right;margin:5px 0;">${text}</div>`;
  
  const reply = Object.keys(responses).find(key => text.includes(key)) 
               ? responses[Object.keys(responses).find(key => text.includes(key))] 
               : "这个问题我还需要学习，请联系管理员获取帮助~";
  
  chatArea.innerHTML += `<div class="bot-msg" style="margin:5px 0;">${reply}</div>`;
  document.getElementById('user-input').value = '';
  chatArea.scrollTop = chatArea.scrollHeight;
}
</script>

<style>
.bot-msg { background: #f1f1f1; padding:8px; border-radius:5px; display:inline-block; max-width:80%; }
.user-msg { color: white; background: #007bff; padding:8px; border-radius:5px; display:inline-block; }
</style>
