<template>
    <div class="test">
        <!--图片上传测试-->
        <div class="c_hide">
            <input class="file" name="file" type="file" accept="image/png,image/gif,image/jpeg" @change="update"/>
            <div class="c_p_10">
                {{ now }}
            </div>
        </div>
        <!--选择省市区测试-->
        <div class="c_box c_w">
            <c-area @saveAddrClick="saveAddrClick" :addrtemp="addr" :province="province" :city="city" :district="district">
            </c-area>
        </div>
    </div>
</template>

<script>
    // import axios from 'axios'
    import cArea from './c-area'

    export default {
        name: "test",
        components: {
            cArea
        },
        data: function () {
            return {
                token: 'nLz_K4jIYyzL_DkVjj5IUq4ZV6NnQdZkzYUyrdEZ:3umhSwnqPzmR7y_1Xp1TXFD3ZOs=:eyJzY29wZSI6ImR6bW9zczo0NjI5NjM4ODQ3MjkwODg0MTUwIiwiZGVhZGxpbmUiOjE1NDIxMTE5NTl9',
                fileid: '4629638847290884150',
                //选择省市区
                province:'',
                city:'',
                district:'',
                addr: {},
            };
        },
        computed: {
            now: function () {
                return Date.now();
            }
        },
        mounted: function () {
            // this.$ajax.get(this.$$api.mobile.getimgtoken, {}, (res) => {
            //   this.token = res.data.token;
            //   this.fileid = res.data.fileid;
            // });
        },
        methods: {
            update(e) {
                let file = e.target.files[0];
                let param = new FormData(); //创建form对象
                param.append('file', file, file.name);//通过append向form对象添加数据
                param.append('chunk', '0');//添加form表单中其他数据
                param.append('token', this.token);//添加form表单中其他数据
                param.append('key', this.fileid);//添加form表单中其他数据
                console.log(param.get('file')); //FormData私有类对象，访问不到，可以通过get判断值是否传进去
                let config = {
                    headers: {'Content-Type': 'multipart/form-data'}
                };
                // axios.post('http://up-z1.qiniup.com/', param, config)
                //   .then(response => {
                //     console.log(response.data);
                //   });
            },
            pic: function () {
                //_____
                (function () {
                    var Watermark = function (obj, img, options) {//可选参数
                        this.can = obj;
                        this.text = options.text || '';
                        this.arrImg = options.arrImg || '';
                        this.left = options.left || 0;
                        this.width = options.width || 0;
                        this.height = options.height || 0;
                        this.top = options.top || 0;
                        this.color = options.color || '#000';
                        this.img = img;
                        this.family = options.family || '12px Microsoft YaHei';
                        this.init();
                    };
                    Watermark.prototype = {
                        init: function () {
                            this.draw();
                        },
                        draw: function () {
                            var canvas = this.can;
                            var ctx = canvas.getContext("2d");
                            if (this.text) {//如果是文本
                                var oImg;
                                if (typeof this.img == 'object') {//如果是img对象
                                    oImg = this.img;
                                    ctx.drawImage(oImg, 0, 0);//直接显示
                                } else if (typeof this.img == 'string') {//如果传入的事路径
                                    var newImg = new Image();//创建图片
                                    newImg.src = this.img;
                                    oImg = newImg;
                                }
                                ctx.drawImage(oImg, 0, 0);
                                ctx.font = this.family;//文字样式
                                ctx.fillStyle = this.color;//设置文字颜色
                                ctx.fillText(this.text, this.left, this.top); //追加文字
                            } else {//如果是水印图片
                                ctx.drawImage(this.img, 0, 0);//直接在canvas上drawImage两个图片
                                ctx.drawImage(this.arrImg, this.left, this.top, this.width, this.height);
                            }
                        },
                        getImg: function () //获取图片路径
                        {
                            var image = this.can.toDataURL("image/png");
                            return image.substring(22);
                        },
                        downImg: function () { //下载图片
                            var image = this.can.toDataURL("image/png").replace("image/png", "image/octet-stream");
                            window.location.href = image;
                        }
                    }
                    window.Watermark = Watermark;
                })()
                // 调用：
//文字水印
                var img = new Watermark(canvas, newImgs, {
                    text: '你大爷', left: 50, top: 50, color: '#fff', family: 'italic small-caps bold 20px 楷体',
                    width: newImgs2.width,
                    height: newImgs2.height
                });

//图片水印
                var img2 = new Watermark(canvas1, newImgs, {
                    arrImg: newImgs2, left: 50, top: 50,
                    width: newImgs2.width,
                    height: newImgs2.height
                });
                // 参数预览：
//参数设置
                /*{
                canvas == canvas对象
                newImgs == img对象或img图片路径
                {
                text/arrImg : 文本 显示在图像上的文字/img对象(该参数如果传入text文本 将显示水印，如果传入arrImg对象 将显示传入的img)
                left: 文字的left位置
                top:文字的top文字
                color:'文字的颜色'
                family:'文字的样式--大小-字体--粗细' （注：这个根据css的 font属性来设置 font:...）
                }
                }*/

//方法
//getImg()//获取图片的Base64编码路径
//downImg()//下载图片

//var url = img.getImg();//获取图片路径并把该路径上传到后台 后台通过Base64解码 得到图片


                //_____
            },
            // 选择省市区
            saveAddrClick:function (addr) {
                this.province = addr.province;
                this.city = addr.city;
                this.district = addr.district;
                this.addr = Object.assign({},addr);
            }

        },
    }
</script>

<style scoped>
    .item-header{
        width: 100%;
        background: #f7f7f7;
        padding: 10px;
        box-sizing: border-box;
    }
    >>>.item-group {
        width: 100%;
        box-sizing: border-box;
        word-wrap: break-word;
        padding: 3.226vw;
        display: flex;
        justify-content: space-between;
    }

    .item-title {
        text-align: left;
        height: 100%;
    }

    .item-content {
        width: 65%;
        text-align: right;
        font-size: 3.5vw;
        /*background: blue;*/
        white-space: nowrap;
        text-overflow: ellipsis;
    }

    .item-content input {
        font-size: 3.5vw;
    }

    .item-value {
        width: 90%;
        display: inline-block;
        height: 100%;
        padding: 0;
        margin: 0;
    }

    .item-value input {
        width: 100%;
        height: 100%;
        border: none;
        outline: none;
        text-align: right;
        padding: 0;
        margin: 0;
        display: flex;
        align-content: center;
        /*background: red;*/
    }
</style>
