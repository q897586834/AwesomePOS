<template>
  <div class="left-nav">
    <ul>
      <li>
        <i class="icon iconfont icon-gouwu"></i>
        <div>收银</div>
      </li>
      <li>
        <i class="icon iconfont icon-shouye"></i>
        <div>店铺</div>
      </li>
      <li>
        <i class="icon iconfont icon-burger"></i>
        <div>商品</div>
      </li>
      <li>
        <i class="icon iconfont icon-huiyuan"></i>
        <div>会员</div>
      </li>
      <li>
        <i class="icon iconfont icon-dingdan"></i>
        <div>统计</div>
      </li>
      <li>
        <i class="icon iconfont icon-tools"></i>
        <div>设置</div>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "leftNav",
  data() {
    return {};
  }
};
</script>
<style>
.left-nav {
  color: #fff;
  font-size: 10px;
  height: 100%;
  background-color: #1d8ce0;
  float: left;
  width: 5%;
}
.iconfont {
  font-size: 3rem;
}
.left-nav ul {
  padding: 0px;
  margin: 0px;
}
.left-nav li {
  list-style: none;
  text-align: center;
  border-bottom: 1px solid #20a0ff;
  padding: 10px;
}
</style>