<template>
  <div style="position:relative">
    <Button @click="paintCanvas(1,'single')">合成图片并下载</Button>
    <div id="1" class="qrcode">
      <vue-qr
        :correctLevel="3"
        :logoScale="0.4"
        :logoSrc="config.logo"
        :text="qrCodeText"
        :size="100"
        :margin="0"
        :dotScale="1"
        style="margin: 10px"
      ></vue-qr>
    </div>
    
    <div id="test" ref="box">
      <div id="poster" class="flex-row" style="position:relative">
        <img id="img" style="width:400px;height:500px" class="poster-bg" src="../../../public/images/bg.jpg"/>  
      </div>
    </div>

    <Button @click="batchDownLoad()">压缩并批量下载</Button>
      <div id="batch" hidden class="qrcode">
        <div v-for="item in testList" :key="item.id">
          <div :id="'batch'+item.id">
            <vue-qr
            class="boxqr"
              :correctLevel="3"
              :logoScale="0.4"
              :logoSrc="config.logo"
              :text="item.qrText"
              :size="200"
              :margin="0"
              :dotScale="1"
              style="margin: 10px;"
            ></vue-qr>
          </div>
        </div>
      </div>
      <canvas
        id="box"
        style="display: none;background: #FFFFFF;width: 500px;height: 700px"
        width="400px"
        height="500px"
      >
      </canvas>
  </div>
</template>
    
<script>
/* eslint-disable */
import { qrcanvas } from "qrcanvas";
import html2canvas from "html2canvas";
import VueQr from "vue-qr";
import JSZip from "jszip";
import FileSaver from "file-saver";
import picture from "../../assets/logo.jpg";
export default {
  name: "test",
  components: {
    VueQr,
    JSZip,
    FileSaver
  },
  data() {
    return {
      dataUrls: [],
      qrCodeText: "https://m.tyqjd.cn/addons/we7_wmall/template/vue/index.html?menu=#/tangshi/pages/table/goods?sid=1341&table_id=194&i=8",
      // bgSrc: require("../../../public/images/bj.jpg"),//背景图
      config: {
        logo: picture //中间logo的地址
      },

      testList: [
        {
          title:'101a',
          id: '101a',
          qrText:
            "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=194",
        },
        {
          id: '101b',
          qrText:
            "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=195"
        },  
        {
          id: '102a',
          qrText:
            "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=196"
        },
        {
          id:'102b',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=197"
        },
        {
          id:'103a',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=198"
        },
        {
          id:'103b',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=199"
        },
        {
          id:'104a',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=200"
        },
        {
          id:'104b',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=201"
        },
        {
          id:'105a',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=202"
        },
        {
          id:'105b',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=203"
        },
        {
          id:'106a',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=204"
        },
        {
          id:'106b',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=205"
        },
        {
          id:'107a',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=206"
        },
        {
          id:'107b',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=207"
        },
        {
          id:'108',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=208"
        },
        {
          id:'109',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=210"
        },
        {
          id:'111',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=211"
        },
        {
          id:'112',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=212"
        },
        {
          id:'113',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=213"
        },
        {
          id:'114',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=214"
        },
        {
          id:'201',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=215"
        },
        {
          id:'202',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=216"
        },
        {
          id:'203',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=217"
        },
        {
          id:'204',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=218"
        },
        {
          id:'205',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=219"
        },
        {
          id:'206',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=220"
        },
        {
          id:'207',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=221"
        },
        {
          id:'208',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=222"
        },
        {
          id:'209a',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=223"
        },
        {
          id:'209b',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=224"
        },
        {
          id:'210',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=225"
        },
        {
          id:'301',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=226"
        },
        {
          id:'302',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=227"
        },
        {
          id:'303',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=228"
        },
        {
          id:'304',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=229"
        },
        {
          id:'305',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=230"
        },
        {
          id:'306',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=231"
        },
        {
          id:'307',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=232"
        },
        {
          id:'308',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=253"
        },
        {
          id:'309',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=233"
        },
        {
          id:'310 ',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=234"
        },
        {
          id:'311',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=235"
        },
        {
          id:'312',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=236"
        },
        {
          id:'313',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=237"
        },
        {
          id:'314',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=238"
        },
        {
          id:'315',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=239"
        },
        {
          id:'316',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=240"
        },
        {
          id:'317',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=241"
        },
        {
          id:'318',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=242"
        },
        {
          id:'319',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=243"
        },
        {
          id:'320',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=244"
        },
        {
          id:'321',
          qrText:
          "https://m.tyqjd.cn/app/index.php?i=8&c=entry&ctrl=wmall&ac=store&op=breakfast&do=mobile&m=we7_wmall&sid=1341&table_id=245"
        },
      ]
    };
  },
  methods: {
    paintCanvas(id, type) {
      let c = document.getElementById("box"); //获取canvas画布 画布大小和canvas大小一致
      let picName = "" + id;
      let ctx = c.getContext("2d");
      c.height = c.height; //清空画布，重新绘制
      let div = null;
      if (type != "single") div = document.getElementById("batch" + id);
      else div = document.getElementById(id);
      //背景图
      let div1 = document.getElementById("poster")
      let bgimg = div1.getElementsByTagName("img")[0];//获取图片
      ctx.drawImage(bgimg,0,0,400,500);

      let img = div.getElementsByTagName("img")[0]; //获取图片
      //白色背景
      ctx.fillStyle = "white"//背景色
      // ctx.strokeRect(50.5,50.5,100,100);//对边框的设置
      ctx.fillRect(38,303,155,155);//对内容的设置
      //
      ctx.drawImage(img, 46, 310, 140, 140); //绘制图片， 左，上，宽，高
      ctx.font = "35px bold 微软雅黑"; //设置字体大小
      ctx.fillStyle = "#fff"//设置字体颜色
      
      //多画几次，让字体加粗
      for (let i = 0; i < 10; i++) {
        ctx.fillText(id, 75, 490); //使用偏移量加粗字体
      }       
      let dataUrl = c.toDataURL();
      this.dataUrls.push({ picData: dataUrl, fileName: picName });
      if (type == "single") {
        const link = document.createElement("a");
        link.download = "合成测试.jpg";
        link.href = dataUrl;
        link.click();
      }
    },  
    //批量下载
    batchDownLoad() {
      this.dataUrls = []; //重置dataUrls
      for (const a of this.testList) {
        this.paintCanvas(a.id, "batch");
      }
      this.handleBatchDownload();
    },
    //压缩图片
    handleBatchDownload() {
      const zip = new JSZip();
      const zipName = "餐桌二维码.zip";
      this.dataUrls.forEach(item => {
        const fileName = item.fileName + ".png";
        let arrData = item.picData.split(",");
        zip.file(fileName, arrData[1], { base64: true }); //向zip中添加文件
      });
      //打包压缩
      zip.generateAsync({ type: "blob" }).then(function(content) {
        saveAs(content, zipName);
      });
    }
  }
};
</script>

<style>
.qrcode {
  position: absolute;
  z-index: 100;
  padding: 196px 91px;
}
</style>