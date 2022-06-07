<template>
  <div>
    <input id="text" type="text" value="Runoob" />
    <button id="sendMessage">发送消息</button>
  </div>
  <iframe
    loading="lazy"
    id="receiver"
    src="http://localhost:8082/#/son"
    width="300"
    height="360"
  >
    <p>你的浏览器不支持 iframe。</p>
  </iframe>
</template>
<script>
export default {
  data() {
    return {};
  },
  mounted() {
    this.test();
  },
  methods: {
    test() {
      const receiver = document.getElementById('receiver').contentWindow;
      const btn = document.getElementById('sendMessage');
      btn.addEventListener('click', (e) => {
        e.preventDefault();
        const val = document.getElementById('text').value;
        receiver.postMessage(`Hello ${val}！`, 'http://localhost:8082/#/son');
      });
    },
  },
};
</script>
