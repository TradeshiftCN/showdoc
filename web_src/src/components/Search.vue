<template>
  <div id="wrapper">

    <div class="content tc">
      <p class="logo"><img src="static/logo/TS_logo_2016_blue.png" alt="logo" /></p>

      <div class="searchBox">
        <form id="form" >
          <input type="hidden" name="item_id" value="7">
          <input type="text" id="keyword" class="searchIpt f14" name="keyword" maxlength="100" autocomplete="off"/>
          <input type="button" class="btn cp" @click="submitForm()" value="TS一下" />

        </form>
      </div>
    </div>

  </div>
</template>

<script>
	export default {
		name: "search",
    methods: {
      submitForm() {
        let formdata = new FormData();
        formdata.append('item_id', '7');
        formdata.append('keyword', $("#keyword").val());

        $.ajax({
          type: "POST",
          dataType: "json",
          processData: false,
          contentType: false,
          url: "http://kubectl.bwtsi.cn/server/index.php?s=/api/item/info",
          data: formdata,
          success: function (result) {
            console.log(result);//打印服务端返回的数据(调试用)
            let page_id = result.data.menu.pages[0].page_id;
            window.location.href = `http://kubectl.bwtsi.cn/web/#/7?page_id=${page_id}`;
          },
          error: function () {
            alert("异常！");
          }
        });
      }
    },
    mounted() {
      var that = this;

    }
	}

</script>

<style scoped>

</style>
