# 郑州市专业技术人员继续教育刷课脚本


## 脚本

学习网站：学习网站：zzzj.hnhhlearning.com, zzzj.jxjyedu.org.cn

脚本地址：[郑州市专业技术人员继续教育刷课脚本][2]

## 教程

浏览器安装篡改猴插件后，打开[脚本安装地址][2]，进入后点击安装脚本，安装完成刷新你的学习网页就可以愉快使用了。

## 代学

注：如果需要代学，可以联系我微信yizhituziang或者QQ2422270452。

微信二维码：  
![微信二维码](https://www.tuziang.com/wx.jpg)

## 代码

关键代码分享：
```

    function open(){
        window.location.reload();
    }

    // 监听，如果窗口变为活跃，那么强制刷新页面
    function isFocus(){
        if(!document.hidden){
            window.location.reload();
            console.log("Refresh the course status!");
        }
    }
    document.addEventListener("visibilitychange", isFocus);

    function coursesPage(){
		if(document.URL.search('yanxiu.qlteacher.com/project/yey2023/learning/learning')>1 ||
           document.URL.search('yanxiu.qlteacher.com/project/xx2023/learning/learning')>1 ||
           document.URL.search('yanxiu.qlteacher.com/project/cz2023/learning/learning')>1 ||
           document.URL.search('yanxiu.qlteacher.com/project/gz2023/learning/learning')>1){
            // 当且仅当窗口活跃
            if(!document.hidden){
                setTimeout(console.log("mainpage waiting..."), 500);
                var courseList1 = $("a:contains('继续学习')");
                var courseList2 = $("a:contains('开始学习')");
                var courseList3 = $("a:contains('温故知新')");
                if(courseList1.length) courseList1[0].click();
                else if(courseList2.length) courseList2[0].click();
                // else if(courseList3.length) courseList3[0].click();
            }
		}
    }
    setInterval(coursesPage, 3000)

    function coursePage(){
        var patt = /^https:\/\/player.qlteacher.com\/learning\/.*=.*/;
        if(document.URL.match(patt) == document.URL){
            var buttons = document.getElementsByTagName("button");
            for(var i=0; i<buttons.length; i++){
                var spans = buttons[i].getElementsByTagName("span");
                for(var j=0; j<spans.length; j++){
                    if(spans[j].innerText){
                        if(spans[j].innerText.includes("继续学习")){
                            buttons[i].click();
                        }
                        if(spans[j].innerText.includes("开始学习")){
                            buttons[i].click();
                        }
                        if(spans[j].innerText.includes("已完成学习")){
                            window.close();
                        }
                    }
                }
            }
		}
    }
    setInterval(coursePage, 1000);

    function play(){
        var patt = /^https:\/\/player.qlteacher.com\/learning\/[^=]*/;
        if(document.URL.match(patt) == document.URL){

            // 纯测试题的课程
            if(document.getElementsByClassName("segmented-text-ellipsis mr-16").length > 0 &&
               document.getElementsByClassName("segmented-text-ellipsis mr-16")[0].innerText == "测试题"){

                // 拿到所有题目，并为每个题选择第一个选项（这里的题目不要求全部做对才算完成）
                var tests = document.getElementsByClassName("mb-16 ng-star-inserted");
                for(var t=0; t<tests.length; t++){
                    tests[t].querySelectorAll("label")[0].click();
                }

                // 提交答案
                var buttons = document.querySelectorAll("button");
                for(var k=0; k<buttons.length; k++){
                    if(buttons[k].getElementsByClassName("ng-star-inserted").length > 0 &&
                       buttons[k].getElementsByClassName("ng-star-inserted")[0].innerText == "提交"){
                        buttons[k].click();
                        break;
                    }
                }

                // 确定提交
                buttons = document.querySelectorAll("button");
                for(k=0; k<buttons.length; k++){
                    if(buttons[k].getElementsByClassName("ng-star-inserted").length > 0 &&
                       buttons[k].getElementsByClassName("ng-star-inserted")[0].innerText == "确定"){
                        buttons[k].click();
                        break;
                    }
                }

                // 如果状态为已完成，则关闭窗口
                if(document.getElementsByClassName('count-down ng-star-inserted')[0].innerText=="已完成"){
                    window.close();
                }
            }

            // 弹出的多选题窗口，每次随机选择
            else if(document.getElementsByClassName("ant-checkbox").length > 0){
                document.getElementsByTagName('video')[0].paused==true;
                var items1 = document.getElementsByClassName("ant-checkbox");
                var cnt = 0;
                for(var i=0; i<items1.length; i++){
                    var randomZeroOrOne = Math.floor(Math.random() * 2 + 0.5);
                    if(randomZeroOrOne == 1) {
                        cnt++;
                        items1[i].click();
                    }
                }
                if(cnt > 0){
                    document.getElementsByClassName("ant-btn radius-4 px-lg py0 ant-btn-primary")[0].click();
                }
            }

            // 弹出的单选题窗口，每次随机选择一个选项
            else if(document.getElementsByClassName("ant-radio-input").length > 0){
                document.getElementsByTagName('video')[0].paused==true;
                var options = document.getElementsByClassName("ant-radio-input");
                var randomIndex = Math.floor(Math.random() * options.length);
                options[randomIndex].click();
                document.getElementsByClassName("ant-btn radius-4 px-lg py0 ant-btn-primary")[0].click();
            }

            // 播放视频
            else if(document.getElementsByTagName('video').length > 0 &&
               document.getElementsByTagName('video')[0].paused==true){
                document.getElementsByTagName('video')[0].muted = true;
                document.getElementsByTagName('video')[0].play();
                //document.querySelector('video').playbackRate = 16;//设置播放速度
            }

            // 如果完成，则退出
            if(document.getElementsByClassName('count-down ng-star-inserted')[0].innerText=="已完成"){
                window.close();
			}
		}
    }
    setInterval(play, 1000)
```


  [1]: https://microsoftedge.microsoft.com/addons/detail/%E7%AF%A1%E6%94%B9%E7%8C%B4/iikmkjmpaadaobahmlepeloendndfphd?refid=bingshortanswersdownload
  [2]: https://greasyfork.org/zh-CN/scripts/403609-%E9%83%91%E5%B7%9E%E5%B8%82%E4%B8%93%E4%B8%9A%E6%8A%80%E6%9C%AF%E4%BA%BA%E5%91%98%E7%BB%A7%E7%BB%AD%E6%95%99%E8%82%B2%E5%88%B7%E8%AF%BE%E8%84%9A%E6%9C%AC
