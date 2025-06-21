---
{"dg-publish":true,"permalink":"/浏览器/事件循环 Event Loop/","created":"2025-06-16T22:00:22.441+08:00","updated":"2025-06-21T11:38:15.931+08:00"}
---

# 事件循环
[[前端八股/浏览器/前端面试 浏览器原理篇_w3cschool#6. 对事件循环的理解\|对事件循环的理解]]
所谓Event Loop，就是事件循环，其实就是JS管理事件执行的一个流程，具体的管理办法由他具体的运行环境确定。目前JS的主要运行环境有两个

- 浏览器
-  Node.js

这两个环境的Event Loop是有区别的

## 浏览器的进程模型

[[前端八股/浏览器/前端面试 浏览器原理篇_w3cschool#二、进程与线程\|进程与线程]]

### 何为进程？

程序运行需要有它自己专属的内存空间，可以把这块内存空间简单的理解为进程

![attachments/20250621104020.png](/img/user/%E6%B5%8F%E8%A7%88%E5%99%A8/attachments/20250621104020.png)
每个应用至少有一个进程，进程之间相互独立，即使要通信，也需要双方同意。

### 何为线程？

有了进程后，就可以运行程序的代码了。

运行代码的「人」称之为「线程」。

一个进程至少有一个线程，所以在进程开启后会自动创建一个线程来运行代码，该线程称之为主线程。

如果程序需要同时执行多块代码，主线程就会启动更多的线程来执行代码，所以一个进程中可以包含多个线程。
![attachments/20250621104041.png](/img/user/%E6%B5%8F%E8%A7%88%E5%99%A8/attachments/20250621104041.png)
### 浏览器有哪些进程和线程？
[[前端八股/浏览器/前端面试 浏览器原理篇_w3cschool#**Chrome浏览器的架构图**：\|浏览器进程]]

**浏览器是一个多进程多线程的应用程序**

浏览器内部工作极其复杂。

为了避免相互影响，为了减少连环崩溃的几率，当启动浏览器后，它会自动启动多个进程。

![attachments/Paste-image-20250621-4.png](/img/user/%E6%B5%8F%E8%A7%88%E5%99%A8/attachments/Paste-image-20250621-4.png)
> 可以在浏览器的任务管理器中查看当前的所有进程

![attachments/20250621100806.png](/img/user/%E6%B5%8F%E8%A7%88%E5%99%A8/attachments/20250621100806.png)
其中，最主要的进程有：

1. 浏览器进程
   主要负责界面显示、用户交互、子进程管理等。浏览器进程内部会启动多个线程处理不同的任务。
2. 网络进程
   负责加载网络资源。网络进程内部会启动多个线程来处理不同的网络任务。
3. **渲染进程** 
   渲染进程启动后，会开启一个**渲染主线程**，主线程负责执行 HTML、CSS、JS 代码。
   默认情况下，浏览器会为每个标签页开启一个新的渲染进程，以保证不同的标签页之间不相互影响。
4. GPU进程
   > 将来该默认模式可能会有所改变，一个站点一个进程而不是一个标签页一个进程[chrome官方说明文档](https://chromium.googlesource.com/chromium/src/+/main/docs/process_model_and_site_isolation.md#Modes-and-Availability)
   
   
[[../浏览器进程.canvas|浏览器进程]]

<style> .container {font-family: sans-serif; text-align: center;} .button-wrapper button {z-index: 1;height: 40px; width: 100px; margin: 10px;padding: 5px;} .excalidraw .App-menu_top .buttonList { display: flex;} .excalidraw-wrapper { height: 800px; margin: 50px; position: relative;} :root[dir="ltr"] .excalidraw .layer-ui__wrapper .zen-mode-transition.App-menu_bottom--transition-left {transform: none;} </style><script src="https://cdn.jsdelivr.net/npm/react@17/umd/react.production.min.js"></script><script src="https://cdn.jsdelivr.net/npm/react-dom@17/umd/react-dom.production.min.js"></script><script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@excalidraw/excalidraw@0/dist/excalidraw.production.min.js"></script><div id="浏览器进程excalidraw.md1"></div><script>(function(){const InitialData={"type":"excalidraw","version":2,"source":"https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/2.12.4","elements":[{"id":"ttwrRCDLqCJOfoLwcUyuT","type":"rectangle","x":-347.5,"y":10.5625,"width":154,"height":67,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a0","roundness":{"type":3},"seed":172604116,"version":247,"versionNonce":1788444500,"isDeleted":false,"boundElements":[{"type":"text","id":"CSAPuj05"},{"id":"jtuGj4ePO8tFPRS42KxO2","type":"arrow"},{"id":"upmIg_heqLRJbxJV4Iqj3","type":"arrow"},{"id":"K64Cn91gpVdqK85mxZDTN","type":"arrow"},{"id":"Aoer1teFMzRf1nF2gf4b7","type":"arrow"}],"updated":1750475855310,"link":null,"locked":false},{"id":"CSAPuj05","type":"text","x":-320.5,"y":31.5625,"width":100,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a1","roundness":null,"seed":1460803180,"version":133,"versionNonce":190215380,"isDeleted":false,"boundElements":[],"updated":1750475855310,"link":null,"locked":false,"text":"浏览器进程","rawText":"浏览器进程","fontSize":20,"fontFamily":5,"textAlign":"center","verticalAlign":"middle","containerId":"ttwrRCDLqCJOfoLwcUyuT","originalText":"浏览器进程","autoResize":true,"lineHeight":1.25},{"id":"bHyl_gHCpGK59EujKMtEo","type":"rectangle","x":-86.5,"y":-159.4375,"width":163,"height":59,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a3","roundness":{"type":3},"seed":522859116,"version":65,"versionNonce":1915317356,"isDeleted":false,"boundElements":[{"type":"text","id":"tzhxhBhi"},{"id":"upmIg_heqLRJbxJV4Iqj3","type":"arrow"}],"updated":1750475820005,"link":null,"locked":false},{"id":"tzhxhBhi","type":"text","x":-65,"y":-142.4375,"width":120,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a4","roundness":null,"seed":908567892,"version":21,"versionNonce":241936596,"isDeleted":false,"boundElements":[],"updated":1750475757030,"link":null,"locked":false,"text":"浏览器主进程","rawText":"浏览器主进程","fontSize":20,"fontFamily":5,"textAlign":"center","verticalAlign":"middle","containerId":"bHyl_gHCpGK59EujKMtEo","originalText":"浏览器主进程","autoResize":true,"lineHeight":1.25},{"id":"tcc6QGiaICO3H-B3ZLchQ","type":"rectangle","x":-86.5,"y":-46.4375,"width":171,"height":66,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a5","roundness":{"type":3},"seed":1426870508,"version":42,"versionNonce":1825374060,"isDeleted":false,"boundElements":[{"type":"text","id":"iNuLVd1W"},{"id":"jtuGj4ePO8tFPRS42KxO2","type":"arrow"}],"updated":1750475823876,"link":null,"locked":false},{"id":"iNuLVd1W","type":"text","x":-41,"y":-25.9375,"width":80,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a6","roundness":null,"seed":2074849876,"version":18,"versionNonce":260769108,"isDeleted":false,"boundElements":[],"updated":1750475767690,"link":null,"locked":false,"text":"网络进程","rawText":"网络进程","fontSize":20,"fontFamily":5,"textAlign":"center","verticalAlign":"middle","containerId":"tcc6QGiaICO3H-B3ZLchQ","originalText":"网络进程","autoResize":true,"lineHeight":1.25},{"id":"teQPjR6-K40NDCYY4UFxh","type":"rectangle","x":-94.5,"y":75.5625,"width":175,"height":62,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a7","roundness":{"type":3},"seed":1162739412,"version":54,"versionNonce":1504837740,"isDeleted":false,"boundElements":[{"type":"text","id":"fPTEaCuA"},{"id":"K64Cn91gpVdqK85mxZDTN","type":"arrow"},{"id":"fxXk-eoSfjCZttDjLz6Ui","type":"arrow"}],"updated":1750476848140,"link":null,"locked":false},{"id":"fPTEaCuA","type":"text","x":-47,"y":94.0625,"width":80,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a8","roundness":null,"seed":1418710228,"version":35,"versionNonce":1736229076,"isDeleted":false,"boundElements":[],"updated":1750475861480,"link":null,"locked":false,"text":"渲染进程","rawText":"渲染进程","fontSize":20,"fontFamily":5,"textAlign":"center","verticalAlign":"middle","containerId":"teQPjR6-K40NDCYY4UFxh","originalText":"渲染进程","autoResize":true,"lineHeight":1.25},{"id":"zWL7xBP2ZdX28Wid06bg3","type":"rectangle","x":-89.5,"y":189.5625,"width":161,"height":63,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"a9","roundness":{"type":3},"seed":1520537836,"version":109,"versionNonce":314589012,"isDeleted":false,"boundElements":[{"type":"text","id":"kJotQ338"},{"id":"Aoer1teFMzRf1nF2gf4b7","type":"arrow"}],"updated":1750475862498,"link":null,"locked":false},{"id":"kJotQ338","type":"text","x":-51.079986572265625,"y":208.5625,"width":84.15997314453125,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aA","roundness":null,"seed":1890663404,"version":29,"versionNonce":10826964,"isDeleted":false,"boundElements":[],"updated":1750475862498,"link":null,"locked":false,"text":"GPU进程","rawText":"GPU进程","fontSize":20,"fontFamily":5,"textAlign":"center","verticalAlign":"middle","containerId":"zWL7xBP2ZdX28Wid06bg3","originalText":"GPU进程","autoResize":true,"lineHeight":1.25},{"id":"upmIg_heqLRJbxJV4Iqj3","type":"arrow","x":-192.5,"y":27.711643825756468,"width":104.00757214951477,"height":142.21559624448312,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aB","roundness":{"type":2},"seed":178073684,"version":124,"versionNonce":88117972,"isDeleted":false,"boundElements":[],"updated":1750476880683,"link":null,"locked":false,"points":[[0,0],[104.00757214951477,-142.21559624448312]],"lastCommittedPoint":null,"startBinding":{"elementId":"ttwrRCDLqCJOfoLwcUyuT","focus":0.6506614662942078,"gap":1},"endBinding":{"elementId":"bHyl_gHCpGK59EujKMtEo","focus":0.700515973213305,"gap":2},"startArrowhead":null,"endArrowhead":"arrow","elbowed":false},{"id":"jtuGj4ePO8tFPRS42KxO2","type":"arrow","x":-188.55555812673944,"y":34.81117911924956,"width":94.73445981245295,"height":31.52984301161525,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aC","roundness":{"type":2},"seed":1172167508,"version":190,"versionNonce":1993283668,"isDeleted":false,"boundElements":[],"updated":1750476880695,"link":null,"locked":false,"points":[[0,0],[94.73445981245295,-31.52984301161525]],"lastCommittedPoint":null,"startBinding":{"elementId":"ttwrRCDLqCJOfoLwcUyuT","focus":0.3047944792306517,"gap":4.94444187326053},"endBinding":{"elementId":"tcc6QGiaICO3H-B3ZLchQ","focus":0.2306386658832322,"gap":7.322663558730678},"startArrowhead":null,"endArrowhead":"arrow","elbowed":false},{"id":"K64Cn91gpVdqK85mxZDTN","type":"arrow","x":-190.5,"y":31.373600354608122,"width":88.00000000000001,"height":78.01668000908643,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aD","roundness":{"type":2},"seed":2026747988,"version":157,"versionNonce":259059156,"isDeleted":false,"boundElements":[],"updated":1750476880707,"link":null,"locked":false,"points":[[0,0],[88.00000000000001,78.01668000908643]],"lastCommittedPoint":null,"startBinding":{"elementId":"ttwrRCDLqCJOfoLwcUyuT","focus":-0.8216310959892772,"gap":3},"endBinding":{"elementId":"teQPjR6-K40NDCYY4UFxh","focus":-0.8058479532163741,"gap":8},"startArrowhead":null,"endArrowhead":"arrow","elbowed":false},{"id":"Aoer1teFMzRf1nF2gf4b7","type":"arrow","x":-190.5,"y":32.90234570831606,"width":98,"height":198.97357607113247,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aE","roundness":{"type":2},"seed":258237548,"version":167,"versionNonce":663128276,"isDeleted":false,"boundElements":[],"updated":1750476880719,"link":null,"locked":false,"points":[[0,0],[98,198.97357607113247]],"lastCommittedPoint":null,"startBinding":{"elementId":"ttwrRCDLqCJOfoLwcUyuT","focus":-0.9144061967126113,"gap":3},"endBinding":{"elementId":"zWL7xBP2ZdX28Wid06bg3","focus":-0.925128977178842,"gap":3},"startArrowhead":null,"endArrowhead":"arrow","elbowed":false},{"id":"fxXk-eoSfjCZttDjLz6Ui","type":"arrow","x":81.48931529322448,"y":90.24592657166377,"width":117.51566565879247,"height":40.702172286058044,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aG","roundness":null,"seed":761163628,"version":242,"versionNonce":692716756,"isDeleted":false,"boundElements":null,"updated":1750477073735,"link":null,"locked":false,"points":[[0,0],[117.51566565879247,40.702172286058044]],"lastCommittedPoint":null,"startBinding":{"elementId":"teQPjR6-K40NDCYY4UFxh","focus":-0.7589593249382222,"gap":1.0000002441848614},"endBinding":{"elementId":"n9_fXDrvJlMUBgVARYonU","focus":-0.055013763524547975,"gap":1.9334886405764564},"startArrowhead":null,"endArrowhead":"arrow","elbowed":false},{"id":"n9_fXDrvJlMUBgVARYonU","type":"rectangle","x":200.93846959259344,"y":-11.80610603818974,"width":347.1303725308754,"height":379.5816538156314,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aK","roundness":{"type":3},"seed":257440468,"version":92,"versionNonce":676405972,"isDeleted":false,"boundElements":[{"id":"fxXk-eoSfjCZttDjLz6Ui","type":"arrow"},{"type":"text","id":"X7zcm1u1"}],"updated":1750477060925,"link":null,"locked":false},{"id":"X7zcm1u1","type":"text","x":205.93846959259344,"y":65.48472086962596,"width":216.21998596191406,"height":225,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aKV","roundness":null,"seed":328024556,"version":7,"versionNonce":65538796,"isDeleted":false,"boundElements":null,"updated":1750477070379,"link":null,"locked":false,"text":"- 解析 HTML\n- 解析 CSS\n- 计算样式\n- 布局\n- 处理图层\n- 每秒把页面画 60 次\n- 执行全局 JS 代码\n- 执行事件处理函数\n- 执行计时器的回调函数","rawText":"- 解析 HTML\n- 解析 CSS\n- 计算样式\n- 布局\n- 处理图层\n- 每秒把页面画 60 次\n- 执行全局 JS 代码\n- 执行事件处理函数\n- 执行计时器的回调函数","fontSize":20,"fontFamily":5,"textAlign":"left","verticalAlign":"middle","containerId":"n9_fXDrvJlMUBgVARYonU","originalText":"- 解析 HTML\n- 解析 CSS\n- 计算样式\n- 布局\n- 处理图层\n- 每秒把页面画 60 次\n- 执行全局 JS 代码\n- 执行事件处理函数\n- 执行计时器的回调函数","autoResize":true,"lineHeight":1.25},{"id":"oMe-nG8rRtu8b0V1OX3K6","type":"image","x":182.74592434026522,"y":22.086817517408576,"width":414,"height":418,"angle":0,"strokeColor":"transparent","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aF","roundness":null,"seed":126557780,"version":203,"versionNonce":608803156,"isDeleted":true,"boundElements":[{"id":"fxXk-eoSfjCZttDjLz6Ui","type":"arrow"}],"updated":1750477020874,"link":null,"locked":false,"status":"pending","fileId":"823e3e614026fbb171b3eabf2c2ed820773c1776","scale":[1,1],"crop":null},{"id":"7z3as0B9","type":"text","x":-144.22515861799363,"y":477.91322971358346,"width":8,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aH","roundness":null,"seed":1115539796,"version":7,"versionNonce":1692156652,"isDeleted":true,"boundElements":null,"updated":1750476971864,"link":null,"locked":false,"text":"","rawText":"","fontSize":20,"fontFamily":5,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"","autoResize":true,"lineHeight":1.25},{"id":"6at1x3nw","type":"text","x":-318.2820309635034,"y":545.7659087635282,"width":486.59659045938065,"height":73.18523584706202,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aI","roundness":null,"seed":1077593324,"version":88,"versionNonce":1214872276,"isDeleted":true,"boundElements":null,"updated":1750477016426,"link":"![[../浏览器进程.canvas]]","locked":false,"text":"📍[[浏览器进程\|浏览器进程]]","rawText":"[[../浏览器进程.canvas|浏览器进程]]","fontSize":58.548188677649605,"fontFamily":5,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"📍[[浏览器进程\|浏览器进程]]","autoResize":true,"lineHeight":1.25},{"id":"Q4ACTG0g","type":"text","x":209.78881903389066,"y":129.79948502256394,"width":8,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aJ","roundness":null,"seed":48702060,"version":3,"versionNonce":2075817836,"isDeleted":true,"boundElements":null,"updated":1750477034514,"link":null,"locked":false,"text":"","rawText":"","fontSize":20,"fontFamily":5,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"","autoResize":true,"lineHeight":1.25},{"id":"vnr0Crg5","type":"text","x":248.14033327951137,"y":66.86366677334007,"width":216.21998596191406,"height":225,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aL","roundness":null,"seed":283154668,"version":5,"versionNonce":62033132,"isDeleted":true,"boundElements":null,"updated":1750477059677,"link":null,"locked":false,"text":"- 解析 HTML\n- 解析 CSS\n- 计算样式\n- 布局\n- 处理图层\n- 每秒把页面画 60 次\n- 执行全局 JS 代码\n- 执行事件处理函数\n- 执行计时器的回调函数","rawText":"- 解析 HTML\n- 解析 CSS\n- 计算样式\n- 布局\n- 处理图层\n- 每秒把页面画 60 次\n- 执行全局 JS 代码\n- 执行事件处理函数\n- 执行计时器的回调函数","fontSize":20,"fontFamily":5,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"- 解析 HTML\n- 解析 CSS\n- 计算样式\n- 布局\n- 处理图层\n- 每秒把页面画 60 次\n- 执行全局 JS 代码\n- 执行事件处理函数\n- 执行计时器的回调函数","autoResize":true,"lineHeight":1.25},{"id":"TcXrlhbO","type":"text","x":520.5344216394335,"y":373.6757807383064,"width":8,"height":25,"angle":0,"strokeColor":"#1e1e1e","backgroundColor":"transparent","fillStyle":"solid","strokeWidth":2,"strokeStyle":"solid","roughness":1,"opacity":100,"groupIds":[],"frameId":null,"index":"aM","roundness":null,"seed":10361452,"version":3,"versionNonce":1108569964,"isDeleted":true,"boundElements":null,"updated":1750477047275,"link":null,"locked":false,"text":"","rawText":"","fontSize":20,"fontFamily":5,"textAlign":"left","verticalAlign":"top","containerId":null,"originalText":"","autoResize":true,"lineHeight":1.25}],"appState":{"theme":"light","viewBackgroundColor":"#ffffff","currentItemStrokeColor":"#1e1e1e","currentItemBackgroundColor":"transparent","currentItemFillStyle":"solid","currentItemStrokeWidth":2,"currentItemStrokeStyle":"solid","currentItemRoughness":1,"currentItemOpacity":100,"currentItemFontFamily":5,"currentItemFontSize":20,"currentItemTextAlign":"left","currentItemStartArrowhead":null,"currentItemEndArrowhead":"arrow","currentItemArrowType":"sharp","scrollX":389.08482649388026,"scrollY":465.26359338464846,"zoom":{"value":1.016909},"currentItemRoundness":"round","gridSize":20,"gridStep":5,"gridModeEnabled":false,"gridColor":{"Bold":"rgba(217, 217, 217, 0.5)","Regular":"rgba(230, 230, 230, 0.5)"},"currentStrokeOptions":null,"frameRendering":{"enabled":true,"clip":true,"name":true,"outline":true},"objectsSnapModeEnabled":false,"activeTool":{"type":"selection","customType":null,"locked":false,"fromSelection":false,"lastActiveTool":null}},"files":{}};InitialData.scrollToContent=true;App=()=>{const e=React.useRef(null),t=React.useRef(null),[n,i]=React.useState({width:void 0,height:void 0});return React.useEffect(()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height});const e=()=>{i({width:t.current.getBoundingClientRect().width,height:t.current.getBoundingClientRect().height})};return window.addEventListener("resize",e),()=>window.removeEventListener("resize",e)},[t]),React.createElement(React.Fragment,null,React.createElement("div",{className:"excalidraw-wrapper",ref:t},React.createElement(ExcalidrawLib.Excalidraw,{ref:e,width:n.width,height:n.height,initialData:InitialData,viewModeEnabled:!0,zenModeEnabled:!0,gridModeEnabled:!1})))},excalidrawWrapper=document.getElementById("浏览器进程excalidraw.md1");ReactDOM.render(React.createElement(App),excalidrawWrapper);})();</script>
## 渲染主线程是如何工作的？

渲染主线程是浏览器中最繁忙的线程，需要它处理的任务包括但不限于：

- 解析 HTML
- 解析 CSS
- 计算样式
- 布局
- 处理图层
- 每秒把页面画 60 次
- 执行全局 JS 代码
- 执行事件处理函数
- 执行计时器的回调函数
- ......

> 思考：为什么渲染进程不适用多个线程来处理这些事情？

要处理这么多的任务，主线程遇到了一个前所未有的难题：如何调度任务？

比如：

- 我正在执行一个 JS 函数，执行到一半的时候用户点击了按钮，我该立即去执行点击事件的处理函数吗？
- 我正在执行一个 JS 函数，执行到一半的时候某个计时器到达了时间，我该立即去执行它的回调吗？
- 浏览器进程通知我“用户点击了按钮”，与此同时，某个计时器也到达了时间，我应该处理哪一个呢？
- ......

渲染主线程想出了一个绝妙的主意来处理这个问题：排队!
![attachments/Paste-image-20250621-1.png](/img/user/%E6%B5%8F%E8%A7%88%E5%99%A8/attachments/Paste-image-20250621-1.png)

1. 在最开始的时候，渲染主线程会进入一个无限循环
2. 每一次循环会检查消息队列中是否有任务存在。如果有，就取出第一个任务执行，执行完一个后进入下一次循环；如果没有，则进入休眠状态。
3. 其他所有线程（包括其他进程的线程）可以随时向消息队列添加任务。新任务会加到消息队列的末尾。在添加新任务时，如果主线程是休眠状态，则会将其唤醒以继续循环拿取任务

这样一来，就可以让每个任务有条不紊的、持续的进行下去了。

**整个过程，被称之为事件循环（消息循环）**

## 若干解释

### 何为异步？

代码在执行过程中，会遇到一些无法立即处理的任务，比如：

- 计时完成后需要执行的任务 —— `setTimeout`、`setInterval`
- 网络通信完成后需要执行的任务 -- `XHR`、`Fetch`
- 用户操作后需要执行的任务 -- `addEventListener`

如果让渲染主线程等待这些任务的时机达到，就会导致主线程长期处于「阻塞」的状态，从而导致浏览器「卡死」
![attachments/Paste-image-20250621-3.png](/img/user/%E6%B5%8F%E8%A7%88%E5%99%A8/attachments/Paste-image-20250621-3.png)
**渲染主线程承担着极其重要的工作，无论如何都不能阻塞！**

因此，浏览器选择**异步**来解决这个问题
![attachments/Paste-image-20250621-2.png](/img/user/%E6%B5%8F%E8%A7%88%E5%99%A8/attachments/Paste-image-20250621-2.png)
使用异步的方式，**渲染主线程永不阻塞**

> 面试题：如何理解 JS 的异步？
>
> 
>
> 参考答案：
>
> JS是一门单线程的语言，这是因为它运行在浏览器的渲染主线程中，而渲染主线程只有一个。
>
> 而渲染主线程承担着诸多的工作，渲染页面、执行 JS 都在其中运行。
>
> 如果使用同步的方式，就极有可能导致主线程产生阻塞，从而导致消息队列中的很多其他任务无法得到执行。这样一来，一方面会导致繁忙的主线程白白的消耗时间，另一方面导致页面无法及时更新，给用户造成卡死现象。
>
> 所以浏览器采用异步的方式来避免。具体做法是当某些任务发生时，比如计时器、网络、事件监听，主线程将任务交给其他线程去处理，自身立即结束任务的执行，转而执行后续代码。当其他线程完成时，将事先传递的回调函数包装成任务，加入到消息队列的末尾排队，等待主线程调度执行。
>
> 在这种异步模式下，浏览器永不阻塞，从而最大限度的保证了单线程的流畅运行。

### JS为何会阻碍渲染？

先看代码

```html
<h1>Mr.Yuan is awesome!</h1>
<button>change</button>
<script>
  var h1 = document.querySelector('h1');
  var btn = document.querySelector('button');

  // 死循环指定的时间
  function delay(duration) {
    var start = Date.now();
    while (Date.now() - start < duration) {}
  }

  btn.onclick = function () {
    h1.textContent = '袁老师很帅！';
    delay(3000);
  };
</script>
```

点击按钮后，会发生什么呢？

<见具体演示>

### 任务有优先级吗？

任务没有优先级，在消息队列中先进先出

但**消息队列是有优先级的**

根据 W3C 的最新解释:

- 每个任务都有一个任务类型，同一个类型的任务必须在一个队列，不同类型的任务可以分属于不同的队列。
  在一次事件循环中，浏览器可以根据实际情况从不同的队列中取出任务执行。
- 浏览器必须准备好一个微队列，微队列中的任务优先所有其他任务执行
  https://html.spec.whatwg.org/multipage/webappapis.html#perform-a-microtask-checkpoint

> 随着浏览器的复杂度急剧提升，W3C 不再使用宏队列的说法

在目前 chrome 的实现中，至少包含了下面的队列：

- 延时队列：用于存放计时器到达后的回调任务，优先级「中」
- 交互队列：用于存放用户操作后产生的事件处理任务，优先级「高」
- 微队列：用户存放需要最快执行的任务，优先级「最高」

> 添加任务到微队列的主要方式主要是使用 Promise、MutationObserver
>
> 
>
> 例如：
>
> ```js
> // 立即把一个函数添加到微队列
> Promise.resolve().then(函数)
> ```

> 浏览器还有很多其他的队列，由于和我们开发关系不大，不作考虑

> 面试题：阐述一下 JS 的事件循环
>
> 
>
> 参考答案：
>
> 事件循环又叫做消息循环，是浏览器渲染主线程的工作方式。
>
> 在 Chrome 的源码中，它开启一个不会结束的 for 循环，每次循环从消息队列中取出第一个任务执行，而其他线程只需要在合适的时候将任务加入到队列末尾即可。
>
> 过去把消息队列简单分为宏队列和微队列，这种说法目前已无法满足复杂的浏览器环境，取而代之的是一种更加灵活多变的处理方式。
>
> 根据 W3C 官方的解释，每个任务有不同的类型，同类型的任务必须在同一个队列，不同的任务可以属于不同的队列。不同任务队列有不同的优先级，在一次事件循环中，由浏览器自行决定取哪一个队列的任务。但浏览器必须有一个微队列，微队列的任务一定具有最高的优先级，必须优先调度执行。

> 面试题：JS 中的计时器能做到精确计时吗？为什么？
>
> 
>
> 参考答案：
>
> 不行，因为：
>
> 1. 计算机硬件没有原子钟，无法做到精确计时
> 2. 操作系统的计时函数本身就有少量偏差，由于 JS 的计时器最终调用的是操作系统的函数，也就携带了这些偏差
> 3. 按照 W3C 的标准，浏览器实现计时器时，如果嵌套层级超过 5 层，则会带有 4 毫秒的最少时间，这样在计时时间少于 4 毫秒时又带来了偏差
> 4. 受事件循环的影响，计时器的回调函数只能在主线程空闲时运行，因此又带来了偏差