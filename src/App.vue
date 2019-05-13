<template>
  <div id="app">
    <div id="nav">
      <!--<router-link to="/">Home</router-link>-->
      <!--|-->
      <!--<router-link to="/about">About</router-link>-->
      <!--|-->
      <!--<router-link to="/test">test</router-link>-->
    </div>
    <router-view/>
  </div>
</template>

<style>
  #app {
    /*font-family: "Microsoft YaHei", "SimSun", Helvetica, Arial, sans-serif;*/
    /*-webkit-font-smoothing: antialiased;*/
    /*-moz-osx-font-smoothing: grayscale;*/
    /*!*text-align: center;*!*/
    /*color: #33475A;*/
    /*!*margin-top: 60px;*!*/
    /*width: 100vw;*/
    /*overflow: hidden;*/
  }
  body{
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  a{
    text-decoration: none
  }

  #app .c_size_10{ font-size: 3.226vw;}

  #app .c_hide{ display: none !important;}
  #app .c_p_10{ padding: 2vw;}
  #app .c_p_t_10{ padding-top: 2vw;}
  #app .c_p_b_10{ padding-bottom: 2vw;}
  #app .c_p_l_10{ padding-left: 2vw;}
  #app .c_p_r_10{ padding-right:2vw;}
  #app .c_m_10{ margin: 2vw;}
  #app .c_m_b_10{ margin-bottom:2vw;}
  #app .c_m_t_10{ margin-top: 2vw;}
  #app .c_m_l_10{ margin-left: 2vw;}
  #app .c_m_r_10{ margin-right: 2vw;}
  #app .c_m_t_1{ margin-top: 1vw;}
  #app .c_m_l_1{ margin-left: 1vw;}

  /*主色*/
  #app .c_white{color:#fff !important;}
  #app .c_red{color:red !important;}
  #app .c_green{color:rgb(3,162,228) !important;}
  #app .c_blue{color:rgb(3,162,228); }
  #app .c_blue_dark{color:rgb(3,161,193); }
  #app .c_orange{color:rgb(242,98,53); }
  #app .c_gray{color:rgb(184,195,206); }
  #app .c_gray_drak{color:rgb(108,125,135); }
  #app .c_black{color:rgb(51,71,71); }
  #app .c_star{color:rgb(51,71,71); }
  /*主色*/
  #app .bg_blue{background:rgb(3,162,228); }
  #app .bg_blue_dark{background:rgb(3,161,193); }
  #app .bg_orange{background:rgb(242,98,53); }
  #app .bg_gray{background:rgb(184,195,206); }
  #app .bg_gray_drak{background:rgb(108,125,135); }
  #app .bg_black{background:rgb(51,71,71); }
  #app .bg_yellow{background:rgb(253,185,51); }
  #app .bg_transparent{ background:transparent;}
  #app .bg_white{ background:#fff;}
  /*辅助色*/
  #app .c_pink{color:rgb(243,125,131); }
  #app .c_yellow{color:rgb(189,200,65); }
  #app .c_blue_light{color:rgb(9,209,229); }
  #app .c_purple_light{color:rgb(106,120,209); }
  #app .c_blue_navy{color:rgb(42,87,154); }

  #app .c_clear::after,
  #app .c_clear::before,
  #app .c_clear{
    content: '';
    display:block;
    clear:both;
  }
  #app .c_nowrap{
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  #app .c_nowrap_normal{
    white-space: normal;
  }
  #app .c_rela{ position: relative;}
  #app .c_no_pointer{ pointer-events: none;}
  #app .c_opacity{ opacity: 0;}
  #app .c_left{ text-align: left;}
  #app .c_center{ text-align: center;}
  #app .c_right{ text-align: right;}
  #app .c_lf{ float: left;}
  #app .c_rt{float: right;}
  #app .c_flex{display: flex;}
  #app .c_flex_1{flex: 1;}
  #app .c_flex_center{align-items: center;justify-content:center;}
  #app .c_flex_between{justify-content:space-between;}
  #app .c_flex_around{justify-content:space-around;}
  #app .c_item_center{align-items: center;}
  #app .c_break_all{ word-break: break-all;}
  #app .c_input_none{
    border:none;
    outline: none;
    background: transparent;
  }
  #app .c_underline{
    text-decoration: underline;
  }

  /*文本超出指定宽度改为省略号*/
  #app .c_ellipsis{
    display:inline-block;
    vertical-align:bottom;
    margin:0;
    padding:0;
    width:33vw;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space:nowrap;
  }
  /*隐藏滚动条*/
  #app .scroll-hidden{
    -webkit-overflow-scrolling: touch;
    overflow: -moz-scrollbars-none;
    overflow: -moz-scrollbars-none;
  }
  #app .scroll-hidden::-webkit-scrollbar{
    display: none;
  }
</style>

