<!--
 * @Descripttion: unTitle
 * @Author: yizheng.yuan
 * @Date: 2021-07-23 15:49:28
 * @LastEditors: yizheng.yuan
 * @LastEditTime: 2021-07-23 16:02:36
-->
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div id="container" style="width:100%; height:400px;border:1px solid red;"></div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  watch: {
    $route(to, from) {
      console.log('路由变化', to.path, from.path);
    },
  },
  mounted() {
    console.error('每次加载--', Date.now());
    setTimeout(() => {
      this.MP('NmfCIrNZD29GgyaKXBR5awpIm15XVAGP').then((BMap) => {
        console.error('回调', BMap);
        const map = new BMap.Map('container');
        console.log('map', map);
        map.centerAndZoom(new BMap.Point(113.327212, 23.139973), 12); // 初始化地图,设置中心点坐标和地图级别
        map.enableScrollWheelZoom(true); // 开启鼠标滚轮缩放

        // 创建点标记
        const marker1 = new BMap.Marker(new BMap.Point(113.327212, 23.139973));
        // 在地图上添加点标记
        map.addOverlay(marker1);
        // map.setHeading(64.5);
        // map.setTilt(73);

        // 添加控件
        const top_left_control = new BMap.ScaleControl({ anchor: BMAP_ANCHOR_TOP_LEFT });// 左上角，添加比例尺
        const top_left_navigation = new BMap.NavigationControl(); // 左上角，添加默认缩放平移控件
        const top_right_navigation = new BMap.NavigationControl({ anchor: BMAP_ANCHOR_TOP_RIGHT, type: BMAP_NAVIGATION_CONTROL_ZOOM }); // 右上角，仅包含平移和缩放按钮
        /* 缩放控件type有四种类型:
        BMAP_NAVIGATION_CONTROL_SMALL：仅包含平移和缩放按钮；BMAP_NAVIGATION_CONTROL_PAN:仅包含平移按钮；BMAP_NAVIGATION_CONTROL_ZOOM：仅包含缩放按钮 */

        // 添加控件和比例尺
        map.addControl(top_left_control);
        // map.addControl(top_left_navigation);
        map.addControl(top_right_navigation);
      });
    });
  },
  methods: {
    MP(ak) {
      return new Promise(((resolve, reject) => {
        if (!window.BMap) {
          const script = document.createElement('script');
          script.type = 'text/javascript';
          script.src = `http://api.map.baidu.com/api?v=2.0&ak=${ak}&callback=init`;
          script.onerror = reject;
          document.head.appendChild(script);
          console.error('window.BMap', window.BMap);
          setTimeout(() => {
            resolve(window.BMap);
          }, 1000); // 这里延迟1秒是关键，要不显示不出来
        } else {
          resolve(window.BMap);
        }
      }));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
