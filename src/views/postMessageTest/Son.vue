<template>
  <div id="recMessage">Hello World!</div>
</template>
<script>
export default {
  mounted() {
    this.test();
  },
  methods: {
    test() {
      const messageEle = document.getElementById('recMessage');
      window.addEventListener('message', (e) => {
        console.log(e.origin);
        console.log('aaaaaa!!!!');
        console.log(e.data);
        // if (e.origin !== 'https://www.runoob.com') {
        //
        //   return;
        // }
        messageEle.innerHTML = `从${e.origin}收到消息： ${e.data}`;
      });
    },
  },
};
</script>
