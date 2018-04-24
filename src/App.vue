<template>
  <div id="allmap" style="width: 100%; height: 800px"></div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return {
      msg : "",
      message : "123"
    }
  },
  methods:{
      mapReady(){
        //创建Map实例
        var map =new BMap.Map("allmap",{
          enableMapClick:false
        });
        //定义中心点位置变量
        var point = new BMap.Point(105.403119,38.028658);
        //初始化地图并且设置中心坐标和地图级别
        map.centerAndZoom(point,5);
        map.enableScrollWheelZoom(true);
        //自定义地图样式
        map.setMapStyle({
          style: 'light'
        });

        var randomCount = 1;
        //设置所有省会城市
        var citys = ["北京","天津","上海","重庆","石家庄","太原","呼和浩特","哈尔滨","长春","沈阳","济南","南京","合肥","杭州","南昌","福州","郑州","武汉","长沙","广州","南宁","西安","银川","兰州","西宁","乌鲁木齐","成都","贵阳","昆明","拉萨","海口"];

        // 构造数据
        var data = [];
        while (randomCount--) {
          var cityCenter = mapv.utilCityCenter.getCenterByCityName(citys[parseInt(Math.random() * citys.length)]);
          data.push({
            geometry: {
              type: 'Point',
              coordinates: [cityCenter.lng - 2 + Math.random() * 4, cityCenter.lat - 2 + Math.random() * 4]
            },
            count: 30 * Math.random()
          });
        }

        var dataSet = new mapv.DataSet(data);

        var options = {
          fillStyle: 'rgba(255, 50, 50, 0.6)',
          shadowColor: 'rgba(255, 50, 50, 1)',
          shadowBlur: 30,
          globalCompositeOperation: 'lighter',
          methods: {
            click: function (item) {
              console.log(item);
            }
          },
          size: 5,
          draw: 'simple'
        }

        var mapvLayer = new mapv.baiduMapLayer(map, dataSet, options);

        // dataSet.set(data); // 修改数据

        // mapvLayer.show(); // 显示图层
        // mapvLayer.hide(); // 删除图层

      }
  },
  mounted(){
      this.mapReady();
  }

}
</script>
