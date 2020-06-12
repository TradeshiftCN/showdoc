<template>
  <div id="wrapper">

    <div class="content tc">
      <p class="logo"><img src="static/logo/TS_logo_2016_blue.png" alt="logo" /></p>

      <div class="searchBox">
        <form id="form" >
          <input type="hidden" name="item_id" value="7">
          <input type="text" id="keyword" class="searchIpt f14" name="keyword" maxlength="100" autocomplete="off"/>
          <input type="button" class="btn cp" @click="submitForm()" value="嗖一下" />

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
            if(result.data.menu.pages.length > 0) {
              let page_id = result.data.menu.pages[0].page_id;
            } else {
              alert("很抱歉，没有找到与“alecxcaaaaa”相关的内容。");
            }
            window.location.href = `http://kubectl.bwtsi.cn/web/#/7?page_id=${page_id}`;
          },
          error: function () {
            alert("请求异常！");
          }
        });
      }
    },
    mounted() {
      var that = this;
      $('.uname,.topMenus').hover(function(){
        $('.topMenus').stop(true,true).fadeIn(200);
      },function(){
        $('.topMenus').stop(true,true).delay(500).fadeOut(200);
      });

      //搜索框自动补全;
      $('.searchIpt').AutoComplete({
        'data': ['About Me', '审美网', 'abcdefg', 'One', 'Two', 'Three', 'Four', 'Five', 'Six','smwell.com', 'Seven', 'Eight', 'Nine', 'Ten', 'Eleven', 'Twelve'],
        'itemHeight': 24,
        'width': 529
      }).AutoComplete('show');

      $('.ctnerTab a').click(function(){
        if(!$(this).hasClass('on')){
          $('.ctnerTab a').removeClass('on').eq($(this).index()).addClass('on');
          $('.rtNavs').stop(true,true).hide(200).eq($(this).index()).show(300);
        }
      });

      $('.menusWrapper a').click(function(){
        if(!$(this).hasClass('active')){
          $('.menusWrapper a').removeClass('active').eq($(this).index()).addClass('active');
          $('.cbox').stop(true,true).animate({top:318},100).hide().eq($(this).index()).animate({top:0},400).show();
        }
      });

      $('.smallPics a').click(function(){
        if(!$(this).hasClass('active')){
          $('.smallPics a').removeClass('active').eq($(this).index()).addClass('active');
          $('.picLink').stop(true,true).removeClass('active').eq($(this).index()).addClass('active');
        }
      });

      $('.titleT').hover(function(){
        if(!$(this).hasClass('on')){
          $('.titleT').removeClass('on').eq($(this).index()).addClass('on');
          $('.topicB').stop(true,true).hide().eq($(this).index()).show();
        }
      });
    }
	}

</script>

<style scoped>

</style>
