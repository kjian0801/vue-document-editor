<template>
  <div class="main">

    <!-- Top bar -->
    <vue-file-toolbar-menu :content="menu" class="bar" />

    <!-- Document editor -->
    <vue-document-editor class="editor" ref="editor"
      :content.sync="content"
      :overlay="overlay"
      :zoom="zoom"
      :page_format_mm="page_format_mm"
      :page_margins="page_margins"
      :display="display" />

  </div>
</template>

<script>
import VueFileToolbarMenu from 'vue-file-toolbar-menu';
import VueDocumentEditor from '../DocumentEditor/DocumentEditor.vue'
import InvoiceTemplate from './InvoiceTemplate.vue';

export default {
  components: { VueDocumentEditor, VueFileToolbarMenu },

  data () {
    return {
      // This is where the pages content is stored and synced
      content: [
        // Every item below produce a page break
        // '<h1>Hello world!</h1><p>This is a rich-text editor built on top of <span contenteditable="false"><a href="https://vuejs.org/" target="_blank">Vue.js</a></span> using the native <span contenteditable="false"><a href="https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Editable_content" target="_blank"><i>contenteditable</i></a></span> browser implementation and some JavaScript trickery to spread content over paper-sized pages.</p><p>Built-in functionality includes:</p><ul><li>Using Vue.js components as interactive page templates (see next page)</li><li>Word-by-word page splitting with forward and backward propagation (<u>still experimental</u>)</li><li>Native Print compatible</li><li>Dynamic document format and margins in millimeters</li><li>Custom page overlays (headers, footers, page numbers)</li><li>Page breaks</li><li>Smart zoom and page display modes</li><li>Computes text style at caret position</li></ul><p>This library may be useful if you design an application that generate documents and you would let the user to modify them slightly before printing / saving, but with limited / interactive possibilities. It does not intend to replace a proper document editor with full functionality.<br>Make sure this project is suitable to your needs before using it.</p><p>This demo adds:</p><ul><li>The top bar (<span contenteditable="false"><a href="https://github.com/motla/vue-file-toolbar-menu" target="_blank">vue-file-toolbar-menu</a></span> component) and the functions associated with it</li><li>Rewritten history stack (undo/redo) compatible with native commands</li><li>Pinch and trackpad zooming</li></ul><p>Check out the <span contenteditable="false"><a href="https://github.com/motla/vue-document-editor/blob/master/src/Demo/Demo.vue" target="_blank">Demo.vue</a></span> file if you need to add these functionalities to your application.</p><p>The link below is an example of non-editable block set with <code>contenteditable="false"</code>:</p><p style="text-align:center" contenteditable="false"><a href="https://github.com/motla/vue-document-editor">View docs on Github</a>, you can\'t edit me.</p><p>But you can still edit this.</p>',
        // { template: InvoiceTemplate, props: { invoice_number: "AB38052985" } },
        // '<br><br><h1>Headers / footers example</h1><br>Page numbers have been added on every page of this document.<br>Header and footer overlays will be added from page 3 to all subsequent ones.<br><br>Check out the <code>overlay</code> method of the <span contenteditable="false"><a href="https://github.com/motla/vue-document-editor/blob/master/src/Demo/Demo.vue" target="_blank">Demo.vue</a></span> file to customize this.',
        // '<h1>«</h1><div style="width:80%; text-align:justify; margin:auto"><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed non risus. Suspendisse lectus tortor, dignissim sit amet, adipiscing nec, ultricies sed, dolor. Cras elementum ultrices diam. Maecenas ligula massa, varius a, semper congue, euismod non, mi. Proin porttitor, orci nec nonummy molestie, enim est eleifend mi, non fermentum diam nisl sit amet erat. Duis semper. Duis arcu massa, scelerisque vitae, consequat in, pretium a, enim. Pellentesque congue. Ut in risus volutpat libero pharetra tempor. Cras vestibulum bibendum augue. Praesent egestas leo in pede. Praesent blandit odio eu enim. Pellentesque sed dui ut augue blandit sodales. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Aliquam nibh. Mauris ac mauris sed pede pellentesque fermentum. Maecenas adipiscing ante non diam sodales hendrerit.</p><p>Ut velit mauris, egestas sed, gravida nec, ornare ut, mi. Aenean ut orci vel massa suscipit pulvinar. Nulla sollicitudin. Fusce varius, ligula non tempus aliquam, nunc turpis ullamcorper nibh, in tempus sapien eros vitae ligula. Pellentesque rhoncus nunc et augue. Integer id felis. Curabitur aliquet pellentesque diam. Integer quis metus vitae elit lobortis egestas. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Morbi vel erat non mauris convallis vehicula. Nulla et sapien. Integer tortor tellus, aliquam faucibus, convallis id, congue eu, quam. Mauris ullamcorper felis vitae erat. Proin feugiat, augue non elementum posuere, metus purus iaculis lectus, et tristique ligula justo vitae magna.</p><p>Aliquam convallis sollicitudin purus. Praesent aliquam, enim at fermentum mollis, ligula massa adipiscing nisl, ac euismod nibh nisl eu lectus. Fusce vulputate sem at sapien. Vivamus leo. Aliquam euismod libero eu enim. Nulla nec felis sed leo placerat imperdiet. Aenean suscipit nulla in justo. Suspendisse cursus rutrum augue. Nulla tincidunt tincidunt mi. Curabitur iaculis, lorem vel rhoncus faucibus, felis magna fermentum augue, et ultricies lacus lorem varius purus. Curabitur eu amet.</p><p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed non risus. Suspendisse lectus tortor, dignissim sit amet, adipiscing nec, ultricies sed, dolor. Cras elementum ultrices diam. Maecenas ligula massa, varius a, semper congue, euismod non, mi. Proin porttitor, orci nec nonummy molestie, enim est eleifend mi, non fermentum diam nisl sit amet erat. Duis semper. Duis arcu massa, scelerisque vitae, consequat in, pretium a, enim. Pellentesque congue. Ut in risus volutpat libero pharetra tempor. Cras vestibulum bibendum augue. Praesent egestas leo in pede. Praesent blandit odio eu enim. Pellentesque sed dui ut augue blandit sodales. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Aliquam nibh. Mauris ac mauris sed pede pellentesque fermentum. Maecenas adipiscing ante non diam sodales hendrerit.</p><p>Ut velit mauris, egestas sed, gravida nec, ornare ut, mi. Aenean ut orci vel massa suscipit pulvinar. Nulla sollicitudin. Fusce varius, ligula non tempus aliquam, nunc turpis ullamcorper nibh, in tempus sapien eros vitae ligula. Pellentesque rhoncus nunc et augue. Integer id felis. Curabitur aliquet pellentesque diam. Integer quis metus vitae elit lobortis egestas. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Morbi vel erat non mauris convallis vehicula. Nulla et sapien. Integer tortor tellus, aliquam faucibus, convallis id, congue eu, quam. Mauris ullamcorper felis vitae erat. Proin feugiat, augue non elementum posuere, metus purus iaculis lectus, et tristique ligula justo vitae magna.</p><p>Aliquam convallis sollicitudin purus. Praesent aliquam, enim at fermentum mollis, ligula massa adipiscing nisl, ac euismod nibh nisl eu lectus. Fusce vulputate sem at sapien. Vivamus leo. Aliquam euismod libero eu enim. Nulla nec felis sed leo placerat imperdiet. Aenean suscipit nulla in justo. Suspendisse cursus rutrum augue. Nulla tincidunt tincidunt mi. Curabitur iaculis, lorem vel rhoncus faucibus, felis magna fermentum augue, et ultricies lacus lorem varius purus. Curabitur eu amet.</p></div><h1 style="text-align:right">»</h1>',
        // '<h3 style="text-align:center">--- This is a page break. ---</h3>'
        `<div class="theme">2025年02月10日语文测试-173929</div><div class="group"data-id="0"><div class="group-header"><span class="group-no"contenteditable="false">一、</span><span class="group-name"data-id="0">单选题</span></div><div class="ques-item objective"contenteditable="false"data-id="450512"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">1.</span><span style="font-family: 宋体;">若单项式</span><img src="https://img.xkw.com/dksih/formula/7df56844bb27ca38cc899691d70733b1.svg"class="xkw-math-img"><span style="font-family: 宋体;">的系数为</span><img src="https://img.xkw.com/dksih/formula/0a6936d370d6a238a608ca56f87198de.svg"class="xkw-math-img"><span style="font-family: 宋体;">，次数为</span><img src="https://img.xkw.com/dksih/formula/2c94bb12cee76221e13f9ef955b0aab1.svg"class="xkw-math-img"><span style="font-family: 宋体;">，则</span><img src="https://img.xkw.com/dksih/formula/20d6fc9b90f370fbb27552876b650f8f.svg"class="xkw-math-img"><span style="font-family: 宋体;">的值为（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><span style="font-family: 宋体;">－</span><span style="font-family: 'Times New Roman';">1</span></span></td><td>B.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">0</span></span></td><td>C.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">5</span></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">6</span></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450513"><div class="ques-body"><p style="text-align:justify;word-break:break-word;"><span class="ques-no">2.</span><span style="font-family: 宋体;">将多项式</span><img src="https://img.xkw.com/dksih/formula/3db4438928ee64fe964b37290e6f68ad.svg"class="xkw-math-img"><span style="font-family: 宋体;">按</span><img src="https://img.xkw.com/dksih/formula/81dea63b8ce3e51adf66cf7b9982a248.svg"class="xkw-math-img"><span style="font-family: 宋体;">的降幂排列的结果是（）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/dca5be0659fe7afd6ea25ebe918ca2b8.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/19fca0592e213748d136c11e8174d1bf.svg"class="xkw-math-img"></span></td></tr><tr><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/f820cca679d43b77ce84d504333e3231.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/8e908bf64e55857e05f601565e4491ca.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450514"><div class="ques-body"><p style="text-align:justify;word-break:break-word;"><span class="ques-no">3.</span><span style="font-family: 宋体;">有理数</span><img src="https://img.xkw.com/dksih/formula/62ff2912fd8d93b6e692936d95b727c5.svg"class="xkw-math-img"><span style="font-family: 宋体;">在数轴上对应点的位置如图所示，下列式子正确的是（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="4">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><p style="text-align:justify;word-break:break-word;"><img height="36"source-file="https://img.xkw.com/dksih/QBM/editorImg/2024/2/1/76b126d3-df6a-4a82-a9fa-ed3c0c8fdbb4.ai"src="https://img.xkw.com/dksih/QBM/editorImg/2024/2/1/76b126d3-df6a-4a82-a9fa-ed3c0c8fdbb4.png"width="192"></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/399e97f2eee4ecf8e4acc69e9a039826.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/c07e06bc34732528a4a765458fd0e193.svg"class="xkw-math-img"></span></td><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/481ee0d1e39e92a4732eea90225eb94c.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/33ecda7bfb0a2043306bf7707a136ad0.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450515"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">4.</span><img src="https://img.xkw.com/dksih/formula/403919b87872ed67f6dff63a0da5e34b.svg"class="xkw-math-img"><span style="font-family: 宋体;">的值是（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">1</span></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/29418e5014731850c55565b6bf47aa41.svg"class="xkw-math-img"></span></td><td>C.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">2025</span></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/0478de3d1b3bb8e4040f5ee01979d74e.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450516"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">5.</span><span style="font-family: 'Times New Roman';">2024</span><span style="font-family: 宋体;">年</span><span style="font-family: 'Times New Roman';">8</span><span style="font-family: 宋体;">月</span><span style="font-family: 'Times New Roman';">20</span><span style="font-family: 宋体;">日，首部国产</span><span style="font-family: 'Times New Roman';">3</span><span style="font-family: 'Times New Roman';font-style: italic;">A</span><span style="font-family: 宋体;">游戏《黑神话悟空》发行，一经上线，就创下了多项国产游戏的记录，据统计，截止到</span><span style="font-family: 'Times New Roman';">9</span><span style="font-family: 宋体;">月</span><span style="font-family: 'Times New Roman';">9</span><span style="font-family: 宋体;">日，全球销量就已经达到了</span><span style="font-family: 'Times New Roman';">1840</span><span style="font-family: 宋体;">万套以上，在全世界范围内引发了国外玩家读《西游记》“补课”、游戏取景地客流量增长、联名产品卖到断货等破圈效应．</span><span style="font-family: 'Times New Roman';">1840</span><span style="font-family: 宋体;">万套用科学记数法可以表示为（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）万套．</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/cdca4c50ff2d0cf1a7393a8e7d363c57.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/f009a3d5a17dd459fa6a6231298216dd.svg"class="xkw-math-img"></span></td><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/1ec7f9002e3e45625250b605d70da4f6.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/9e76fce18eb4ac32b3b8041a3c707ed8.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450517"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">6.</span><img src="https://img.xkw.com/dksih/formula/4a94acdfb41489d5694b5a64b9e99754.svg"class="xkw-math-img"><span style="font-family: 宋体;">的绝对值是（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="4">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/1985174e05ad371e13cf24d244423da4.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">7</span></span></td><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/4a94acdfb41489d5694b5a64b9e99754.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/b6a5e6c1452add80f47cbb381d94562a.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450518"><div class="ques-body"><p style="text-align:justify;word-break:break-word;"><span class="ques-no">7.</span><span style="font-family: 宋体;">下列式子中正确的是（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/6ddb31e67b626559822b80bb925e1930.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/e2718cf71b9a125f01e916fe9516a882.svg"class="xkw-math-img"></span></td><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/df30ec2409234c25cf2f7f892161e909.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/00616a2621ff385fa4b4186830dfa135.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450519"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">8.</span><span style="font-family: 宋体;">多项式</span><img src="https://img.xkw.com/dksih/formula/54a227742ddfa406f586a0d4975b7cc4.svg"class="xkw-math-img"><span style="font-family: 宋体;">的次数是（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="4">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/acbc6a613224461ade69362d46550474.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">1</span></span></td><td>C.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">6</span></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">3</span></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450588"><div class="ques-body"><p style="text-align:justify;word-break:break-word;"><span class="ques-no">9.</span><span style="font-family: 宋体;">方程</span><img src="https://img.xkw.com/dksih/formula/1c1de23e06191afca6ee998e12a6dde6.svg"class="xkw-math-img"><span style="font-family: 宋体;">与关于</span><img src="https://img.xkw.com/dksih/formula/81dea63b8ce3e51adf66cf7b9982a248.svg"class="xkw-math-img"><span style="font-family: 宋体;">的方程</span><img src="https://img.xkw.com/dksih/formula/4b14c225a40375a7145d8363e425a872.svg"class="xkw-math-img"><span style="font-family: 宋体;">有相同的解，则</span><img src="https://img.xkw.com/dksih/formula/0a6936d370d6a238a608ca56f87198de.svg"class="xkw-math-img"><span style="font-family: 宋体;">的值为（<span style="font-family: 'Times New Roman'"qml-space-size="4">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/5ca7d1107389675d32b56ec097464c14.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/acbc6a613224461ade69362d46550474.svg"class="xkw-math-img"></span></td><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/b8860d9787671b53b1ab68b3d526f5ca.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/61128ab996360a038e6e64d82fcba004.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450589"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">10.</span><span style="font-family: 宋体;">解方程</span><img src="https://img.xkw.com/dksih/formula/801ced5471f8f858945d054a8ae96f17.svg"class="xkw-math-img"><span style="font-family: 宋体;">时，去分母正确的是（）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/1cb0f1ba64c7daba47bc6bd9d90a13cd.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/0a87c0123076ebaa81b86dd6b789e3e3.svg"class="xkw-math-img"></span></td></tr><tr><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/bea442cda45a088b8bdac4b89cd8cef7.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/696b35d256a6eeb3c201a18f407a7fca.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450590"><div class="ques-body"><p style="text-align:justify;word-break:break-word;"><span class="ques-no">11.</span><span style="font-family: 宋体;">若</span><img src="https://img.xkw.com/dksih/formula/00633cdf24e51537b5b3feef0f73d055.svg"class="xkw-math-img"><span style="font-family: 'Times New Roman';"></span><span style="font-family: 宋体;">与</span><span style="font-family: 'Times New Roman';"></span><img src="https://img.xkw.com/dksih/formula/954e056ecf73e46097fc81da97c07acc.svg"class="xkw-math-img"><span style="font-family: 宋体;">互为相反数，则</span><span style="font-style: italic;font-family: 'Times New Roman';">x</span><span style="font-family: 宋体;">的值为（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/2ff388a5b4054bb2409dee600f1b9615.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/4db5276a530b39af132af21d12333e2f.svg"class="xkw-math-img"></span></td><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/08dd1e25420bb85b96dea24e5d16abee.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/29418e5014731850c55565b6bf47aa41.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450591"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">12.</span><span style="font-family: 宋体;">下面是关于</span><img src="https://img.xkw.com/dksih/formula/81dea63b8ce3e51adf66cf7b9982a248.svg"class="xkw-math-img"><span style="font-family: 宋体;">的一元一次方程</span><img src="https://img.xkw.com/dksih/formula/54f671d62c0b259fbffdb270eceda35a.svg"class="xkw-math-img"><span style="font-family: 宋体;">的求解过程，对于每一步的运算，其中依据表述错误的是（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><table style="border-width:0px 0px 0px 0px;border-style:solid;border-color:black;border-collapse: collapse;"><tbody><tr height="21px"><td style="vertical-align:center;border-width:1px 1px 1px 1px;border-style:solid solid solid solid;border-color:black;"><p style="text-align: left;"><span style="font-family: 宋体;">解方程：</span><img src="https://img.xkw.com/dksih/formula/54f671d62c0b259fbffdb270eceda35a.svg"class="xkw-math-img"><span style="font-family: 宋体;">．</span></p><p style="text-align: left;"><span style="font-family: 宋体;">解：去分母，得</span><img src="https://img.xkw.com/dksih/formula/d5686915509e46891137a031db1dd663.svg"class="xkw-math-img"><span style="font-family: 宋体;">．①</span></p><p style="text-align: left;"><span style="font-family: 宋体;">去括号，得</span><img src="https://img.xkw.com/dksih/formula/1293d0f852040f652feacb3c36486d09.svg"class="xkw-math-img"><span style="font-family: 宋体;">．②</span></p><p style="text-align: left;"><span style="font-family: 宋体;">移项，得</span><img src="https://img.xkw.com/dksih/formula/17fe8c221d08893c694f34dd0b836bf1.svg"class="xkw-math-img"><span style="font-family: 宋体;">．③</span></p><p style="text-align: left;"><span style="font-family: 宋体;">合并同类项，得</span><img src="https://img.xkw.com/dksih/formula/5d11a8b820678e9ac9ab06ad53d438f5.svg"class="xkw-math-img"><span style="font-family: 宋体;">．④</span></p><p style="text-align: left;"><span style="font-family: 宋体;">方程两边同时除以</span><span style="font-family: 'Times New Roman';">17</span><span style="font-family: 宋体;">，得</span><img src="https://img.xkw.com/dksih/formula/639c3d2ff5ee566fcc1b69c65712a661.svg"class="xkw-math-img"><span style="font-family: 宋体;">．</span></p></td></tr></tbody></table><p style="text-align: left;"><span></span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><span style="font-family: 宋体;">①分数的基本性质</span></span></td><td>B.&nbsp;<span class="qml-op"><span style="font-family: 宋体;">②乘法分配律</span></span></td></tr><tr><td>C.&nbsp;<span class="qml-op"><span style="font-family: 宋体;">③等式的基本性质</span></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><span style="font-family: 宋体;">④合并同类项法则</span></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450592"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">13.</span><span style="font-family: 宋体;">解方程</span><img src="https://img.xkw.com/dksih/formula/e4b99f9fce9658f9a43ff58ce3a0c8ee.svg"class="xkw-math-img"><span style="font-family: 宋体;">，去分母后正确的是（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/ce2fac4c5d797a839251375888f38b46.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/f91b0b3974d4ac93476902d510e9f36d.svg"class="xkw-math-img"></span></td></tr><tr><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/ae74aacb129bcbfce4207adaadb61e32.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/1bb7eb472c31036da91b4ea2bc8f0060.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450593"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">14.</span><span style="font-family: 宋体;">若关于</span><img src="https://img.xkw.com/dksih/formula/81dea63b8ce3e51adf66cf7b9982a248.svg"class="xkw-math-img"><span style="font-family: 宋体;">的方程</span><img src="https://img.xkw.com/dksih/formula/39471c2ca6e118eaf29840bb686ba7f8.svg"class="xkw-math-img"><span style="font-family: 宋体;">的解是</span><img src="https://img.xkw.com/dksih/formula/99c6875d552e9fff3c7d655f3a59b166.svg"class="xkw-math-img"><span style="font-family: 宋体;">，则</span><img src="https://img.xkw.com/dksih/formula/f0a532e15e232cb4b99a8d4d07c89575.svg"class="xkw-math-img"><span style="font-family: 宋体;">的值为（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">1</span></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/a734873a608f0c070dec80b89d179754.svg"class="xkw-math-img"></span></td><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/376b2df0246eacc901afe3339db455ae.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><span style="font-family: 'Times New Roman';">0</span></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div><div class="ques-item objective"contenteditable="false"data-id="450594"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">15.</span><span style="font-family: 宋体;">在解方程</span><img src="https://img.xkw.com/dksih/formula/9bd104f7e5f060d8b44db249c2a19f87.svg"class="xkw-math-img"><span style="font-family: 宋体;">时，去分母正确的是（</span><span style="font-family: 'Times New Roman';"><span style="font-family: 'Times New Roman'"qml-space-size="3">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span><span style="font-family: 宋体;">）</span></p><div class=" qml-og"><table class="qml-og"style="width:100%"><tbody><tr><td>A.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/3efb5400e24ba38c6377a3042e3fade9.svg"class="xkw-math-img"></span></td><td>B.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/3a09b29eaa20ed2460278332d351ba81.svg"class="xkw-math-img"></span></td></tr><tr><td>C.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/a90054d579419327805dc8d8a872c44d.svg"class="xkw-math-img"></span></td><td colspan="1">D.&nbsp;<span class="qml-op"><img src="https://img.xkw.com/dksih/formula/7896eb2a6147cd0911c3a6c8744ee556.svg"class="xkw-math-img"></span></td></tr></tbody></table></div></div><div class="ques-answer"></div></div></div><div class="group"data-id="1"><div class="group-header"><span class="group-no"contenteditable="false">二、</span><span class="group-name"data-id="1">填空题</span></div><div class="ques-item subjective"contenteditable="false"data-id="450520"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">16.</span><span style="font-family: 宋体;">若</span><img src="https://img.xkw.com/dksih/formula/5929b0946dc3eda13c0b1fa7582e8dc2.svg"class="xkw-math-img"><span style="font-family: 宋体;">与</span><img src="https://img.xkw.com/dksih/formula/5bf7e97cf1003aca890646407696252f.svg"class="xkw-math-img"><span style="font-family: 宋体;">是同类项，则</span><img src="https://img.xkw.com/dksih/formula/72850427e83ff19a24305783e080b280.svg"class="xkw-math-img"><span style="font-family: 宋体;">的值为</span><span class="qml-bk"contenteditable="true"index="1"size="6"type="underline"style="text-decoration:underline"></span><span style="font-family: 宋体;">．</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450521"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">17.</span><span style="font-family: 宋体;">单项式</span><img src="https://img.xkw.com/dksih/formula/084e3c436d3a8f359d028053f1ba483a.svg"class="xkw-math-img"><span style="font-family: 宋体;">的系数是</span><span class="qml-bk"contenteditable="true"index="1"size="10"type="underline"style="text-decoration:underline"></span><span style="font-family: 宋体;">．</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450548"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">18.</span><span style="font-family: 宋体;">“勾股容方”问题起源于《九章算术》，该问题可以描述为：如图</span><span style="font-family: 'Times New Roman';">1</span><span style="font-family: 宋体;">，已知“勾股形”的勾为</span><img src="https://img.xkw.com/dksih/formula/0a6936d370d6a238a608ca56f87198de.svg"class="xkw-math-img"><span style="font-family: 宋体;">，股为</span><img src="https://img.xkw.com/dksih/formula/2c94bb12cee76221e13f9ef955b0aab1.svg"class="xkw-math-img"><span style="font-family: 宋体;">，求“容方”的边长（“勾股形”即直角三角形，“容方”指与此直角三角形有公共直角的内接正方形，即图</span><span style="font-family: 'Times New Roman';">1</span><span style="font-family: 宋体;">中阴影部分）．魏晋时期数学家刘徽利用“出入相补”原理，将图</span><span style="font-family: 'Times New Roman';">2</span><span style="font-family: 宋体;">中的直角三角形及正方形进行重新组合，得到图</span><span style="font-family: 'Times New Roman';">3</span><span style="font-family: 宋体;">中的长方形，从而算出“容方”的边长为</span><span class="qml-bk"contenteditable="true"index="1"size="10"type="underline"style="text-decoration:underline"></span><span style="font-family: 宋体;">（用含</span><img src="https://img.xkw.com/dksih/formula/0a6936d370d6a238a608ca56f87198de.svg"class="xkw-math-img"><span style="font-family: 宋体;">、</span><img src="https://img.xkw.com/dksih/formula/2c94bb12cee76221e13f9ef955b0aab1.svg"class="xkw-math-img"><span style="font-family: 宋体;">的代数式表示）．</span></p><p style="text-align:justify;word-break:break-word;"><img height="150"source-file="https://img.xkw.com/dksih/QBM/editorImg/2025/2/6/151aafdc-1480-4bdb-98dd-c1bfc3e086e5.ai"src="https://img.xkw.com/dksih/QBM/editorImg/2025/2/6/151aafdc-1480-4bdb-98dd-c1bfc3e086e5.png"width="400"></p></div><div class="ques-answer"></div></div></div><div class="group"data-id="2"><div class="group-header"><span class="group-no"contenteditable="false">三、</span><span class="group-name"data-id="2">解答题</span></div><div class="ques-item subjective"contenteditable="false"data-id="450522"><div class="ques-body"><p style="text-align:justify;word-break:break-word;"><span class="ques-no">19.</span><span style="font-family: 宋体;">计算：</span><img src="https://img.xkw.com/dksih/formula/330e344c54703f06cd41cd442316a967.svg"class="xkw-math-img"><span style="font-family: 宋体;">．</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450523"><div class="ques-body"><p style="text-align:justify;word-break:break-word;"><span class="ques-no">20.</span><span style="font-family: 宋体;">先化简，再求值：</span><img src="https://img.xkw.com/dksih/formula/4c63811d1641ffc831d6d71998eebddd.svg"class="xkw-math-img"><span style="font-family: 宋体;">，其中</span><img src="https://img.xkw.com/dksih/formula/2558aeb6ef170ae4df216f0c94049ecd.svg"class="xkw-math-img"><span style="font-family: 宋体;">．</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450524"><div class="ques-body"><p style="text-align:justify;word-break:break-word;"><span class="ques-no">21.</span><span style="font-family: 宋体;">解一元一次方程：</span><img src="https://img.xkw.com/dksih/formula/6494f96b8b30bc3dba1b0ab0c6b6a698.svg"class="xkw-math-img"><span style="font-family: 宋体;">．</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450525"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">22.</span><span style="font-family: 宋体;">先合并同类项，再求代数式的值：</span><img src="https://img.xkw.com/dksih/formula/3d35d9a01fa50dae432fcc4f88946aa8.svg"class="xkw-math-img"><span style="font-family: 宋体;">，其中</span><img src="https://img.xkw.com/dksih/formula/6b108ab31cc093f03cf48ad65429889e.svg"class="xkw-math-img"><span style="font-family: 宋体;">．</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450526"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">23.</span><span style="font-family: 宋体;">先化简，再求值：</span><img src="https://img.xkw.com/dksih/formula/38d92cf27d996c72045cacdae7075986.svg"class="xkw-math-img"><span style="font-family: 宋体;">，其中</span><img src="https://img.xkw.com/dksih/formula/8e258ab9e600435b37465092243d99f6.svg"class="xkw-math-img"><span style="font-family: 宋体;">，</span><img src="https://img.xkw.com/dksih/formula/b86304c3e26200299a0480641525a283.svg"class="xkw-math-img"><span style="font-family: 宋体;">．</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450527"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">24.</span><span style="font-family: 宋体;">已知甲班有</span><span style="font-family: 'Times New Roman';">38</span><span style="font-family: 宋体;">人，乙班有</span><span style="font-family: 'Times New Roman';">40</span><span style="font-family: 宋体;">人，现在需要从甲、乙两班各抽调一些同学参加学农活动，若从甲班抽调的人数是乙班抽调人数的</span><span style="font-family: 'Times New Roman';">2</span><span style="font-family: 宋体;">倍，则甲班剩余人数比乙班剩余人数少</span><span style="font-family: 'Times New Roman';">12</span><span style="font-family: 宋体;">人，请问从甲、乙两班各抽调了多少人？</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450528"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">25.</span><span style="font-family: 宋体;">求</span><img src="https://img.xkw.com/dksih/formula/ce8df3250f9bd0d33a327f1848b293e6.svg"class="xkw-math-img"><span style="font-family: 宋体;">的值，其中</span><img src="https://img.xkw.com/dksih/formula/48cf5b472ab283ed7b4ff3031d264af8.svg"class="xkw-math-img"><span style="font-family: 宋体;">．</span></p></div><div class="ques-answer"></div></div><div class="ques-item subjective"contenteditable="false"data-id="450529"><div class="ques-body"><p style="text-align: left;"><span class="ques-no">26.</span><span style="font-family: 宋体;">某商店有两种节能灯，每个</span><img src="https://img.xkw.com/dksih/formula/5963abe8f421bd99a2aaa94831a951e9.svg"class="xkw-math-img"><span style="font-family: 宋体;">型节能灯比每个</span><img src="https://img.xkw.com/dksih/formula/7f9e8449aad35c5d840a3395ea86df6d.svg"class="xkw-math-img"><span style="font-family: 宋体;">型节能灯的进价少</span><span style="font-family: 'Times New Roman';">25</span><span style="font-family: 宋体;">元，而它们的售后所获利润相同，其中，每个</span><img src="https://img.xkw.com/dksih/formula/5963abe8f421bd99a2aaa94831a951e9.svg"class="xkw-math-img"><span style="font-family: 宋体;">型节能灯的利润率为</span><img src="https://img.xkw.com/dksih/formula/f51efd0ca4b6c3d42afdc6b8feb330a1.svg"class="xkw-math-img"><span style="font-family: 宋体;">，每个</span><img src="https://img.xkw.com/dksih/formula/7f9e8449aad35c5d840a3395ea86df6d.svg"class="xkw-math-img"><span style="font-family: 宋体;">型节能灯的利润率为</span><img src="https://img.xkw.com/dksih/formula/c8ee628efd6b2f7296c106dd5cbae42f.svg"class="xkw-math-img"><span style="font-family: 宋体;">，求两种节能灯的单个进价．</span></p></div><div class="ques-answer"></div></div></div>`
      ],
      zoom: 0.8,
      zoom_min: 0.10,
      zoom_max: 5.0,
      page_format_mm: [210, 297],
      page_margins: "10mm 15mm",
      display: "grid", // ["grid", "vertical", "horizontal"]
      mounted: false, // will be true after this component is mounted
      undo_count: -1, // contains the number of times user can undo (= current position in content_history)
      content_history: [] // contains the content states for undo/redo operations
    }
  },

  created () {
    // Initialize gesture flags
    let start_zoom_gesture = false;
    let start_dist_touch = false;
    let start_zoom_touch = false;

    // Manage ctrl+scroll zoom (or trackpad pinch)
    window.addEventListener("wheel", (e) => {
      if(e.ctrlKey){
        e.preventDefault();
        this.zoom = Math.min(Math.max(this.zoom - e.deltaY * 0.01, this.zoom_min), this.zoom_max);
      }
    }, { passive: false });

    // Manage trackpad pinch on Safari
    window.addEventListener("gesturestart", (e) => {
      e.preventDefault();
      start_zoom_gesture = this.zoom;
    });
    window.addEventListener("gesturechange", (e) => {
      e.preventDefault();
      if(!start_zoom_touch){
        this.zoom = Math.min(Math.max(start_zoom_gesture * e.scale, this.zoom_min), this.zoom_max);
      }
    });
    window.addEventListener("gestureend", () => {
      start_zoom_gesture = false;
    });

    // Manage pinch to zoom for touch devices
    window.addEventListener("touchstart", (e) => {
      if (e.touches.length == 2) {
        e.preventDefault();
        start_dist_touch = Math.hypot(
          e.touches[0].pageX - e.touches[1].pageX,
          e.touches[0].pageY - e.touches[1].pageY
        );
        start_zoom_touch = this.zoom;
      }
    }, { passive: false });
    window.addEventListener("touchmove", (e) => {
      if (start_dist_touch && start_zoom_touch) {
        e.preventDefault();
        let zoom = start_zoom_touch * Math.hypot(
          e.touches[0].pageX - e.touches[1].pageX,
          e.touches[0].pageY - e.touches[1].pageY
        ) / start_dist_touch;
        this.zoom = Math.min(Math.max(zoom, this.zoom_min), this.zoom_max);
      }
    }, { passive: false });
    window.addEventListener("touchend", () => {
      start_dist_touch = false;
      start_zoom_touch = false;
    }, { passive: false });

    // Manage history undo/redo events
    const manage_undo_redo = (e) => {
      switch(e && e.inputType){
        case "historyUndo": e.preventDefault(); e.stopPropagation(); this.undo(); break;
        case "historyRedo": e.preventDefault(); e.stopPropagation(); this.redo(); break;
      }
    }
    window.addEventListener("beforeinput", manage_undo_redo);
    window.addEventListener("input", manage_undo_redo); // in case of beforeinput event is not implemented (Firefox)

    // If your component is susceptible to be destroyed, don't forget to
    // use window.removeEventListener in the Vue.js beforeDestroy handler
  },

  mounted () { this.mounted = true; },

  computed: {

    // This is the menu content
    menu () {
      return [
        // Main commands
        { text: "New", title: "New", icon: "description", click: () => { if(confirm("This will create an empty document. Are you sure?")){ this.content = [""]; this.resetContentHistory(); } } },
        { text: "Print", title: "Print", icon: "print", click: () => window.print() },

        { is: "spacer" },

        // Undo / redo commands
        { title: "Undo", icon: "undo", disabled: !this.can_undo, hotkey: this.isMacLike ? "command+z" : "ctrl+z", click: () => this.undo() },
        { title: "Redo", icon: "redo", disabled: !this.can_redo, hotkey: this.isMacLike ? "shift+command+z" : "ctrl+y", click: () => this.redo() },

        { is: "spacer" },

        // Rich text menus
        { icon: "format_align_left", title: "Align left", active: this.isLeftAligned, disabled: !this.current_text_style, hotkey: this.isMacLike ? "shift+command+l" : "ctrl+shift+l", click: () => document.execCommand("justifyLeft") },
        { icon: "format_align_center", title: "Align center", active: this.isCentered, disabled: !this.current_text_style, hotkey: this.isMacLike ? "shift+command+e" : "ctrl+shift+e", click: () => document.execCommand("justifyCenter") },
        { icon: "format_align_right", title: "Align right", active: this.isRightAligned, disabled: !this.current_text_style, hotkey: this.isMacLike ? "shift+command+r" : "ctrl+shift+r", click: () => document.execCommand("justifyRight") },
        { icon: "format_align_justify", title: "Justify content", active: this.isJustified, disabled: !this.current_text_style, hotkey: this.isMacLike ? "shift+command+j" : "ctrl+shift+j", click: () => document.execCommand("justifyFull") },
        { is: "separator" },
        { icon: "format_bold", title: "Bold", active: this.isBold, disabled: !this.current_text_style, hotkey: this.isMacLike ? "command+b" : "ctrl+b", click: () => document.execCommand("bold") },
        { icon: "format_italic", title: "Italic", active: this.isItalic, disabled: !this.current_text_style, hotkey: this.isMacLike ? "command+i" : "ctrl+i", click: () => document.execCommand("italic") },
        { icon: "format_underline", title: "Underline", active: this.isUnderline, disabled: !this.current_text_style, hotkey: this.isMacLike ? "command+u" : "ctrl+u", click: () => document.execCommand("underline") },
        { icon: "format_strikethrough", title: "Strike through", active: this.isStrikeThrough, disabled: !this.current_text_style, click: () => document.execCommand("strikethrough") },
        { is: "button-color", type: "compact", menu_class: "align-center", disabled: !this.current_text_style, color: this.curColor, update_color: (new_color) => document.execCommand('foreColor', false, new_color.hex8) },
        { is: "separator" },
        { icon: "format_list_numbered", title: "Numbered list", active: this.isNumberedList, disabled: !this.current_text_style, click: () => document.execCommand("insertOrderedList") },
        { icon: "format_list_bulleted", title: "Bulleted list", active: this.isBulletedList, disabled: !this.current_text_style, click: () => document.execCommand("insertUnorderedList") },
        { html: "<b>H1</b>", title: "Header 1", active: this.isH1, disabled: !this.current_text_style, click: () => document.execCommand('formatBlock', false, '<h1>') },
        { html: "<b>H2</b>", title: "Header 2", active: this.isH2, disabled: !this.current_text_style, click: () => document.execCommand('formatBlock', false, '<h2>') },
        { html: "<b>H3</b>", title: "Header 3", active: this.isH3, disabled: !this.current_text_style, click: () => document.execCommand('formatBlock', false, '<h3>') },
        { icon: "format_clear", title: "Clear format", disabled: !this.current_text_style, click () { document.execCommand('removeFormat'); document.execCommand('formatBlock', false, '<div>'); } },
        { icon: "splitscreen", title: "Page break", disabled: !this.current_text_style, click: () => this.insertPageBreak() },
        
        { is: "spacer" },

        { // Format menu
          text: this.current_format_name,
          title: "Format",
          icon: "crop_free",
          chevron: true,
          menu: this.formats.map(([text, w, h]) => {
            return {
              text,
              active: (this.page_format_mm[0] == w && this.page_format_mm[1] == h),
              click: () => { this.page_format_mm = [w, h]; }
            }
          }),
          menu_width: 80,
          menu_height: 280
        },
        { // Margins menu
          text: this.current_margins_name,
          title: "Margins",
          icon: "select_all",
          chevron: true,
          menu: this.margins.map(([text, value]) => {
            return {
              text: text+" ("+value+")",
              active: (this.page_margins == value),
              click: () => { this.page_margins = value; }
            }
          }),
          menu_width: 200,
          menu_class: "align-center"
        },
        { // Zoom menu
          text: Math.floor(this.zoom * 100) + "%",
          title: "Zoom",
          icon: "zoom_in",
          chevron: true,
          menu: [
            ["200%", 2.0],
            ["150%", 1.5],
            ["125%", 1.25],
            ["100%", 1.0],
            ["75%", 0.75],
            ["50%", 0.5],
            ["25%", 0.25]
          ].map(([text, zoom]) => {
            return {
              text,
              active: this.zoom == zoom,
              click: () => { this.zoom = zoom; }
            }
          }),
          menu_width: 80,
          menu_height: 280,
          menu_class: "align-center"
        },
        { // Display mode menu
          title: "Display",
          icon: this.display == "horizontal" ? "view_column" : (this.display == "vertical" ? "view_stream" : "view_module"),
          chevron: true,
          menu: [{
            icon: "view_module",
            active: this.display == "grid",
            click: () => { this.display = "grid"; }
          }, {
            icon: "view_column",
            active: this.display == "horizontal",
            click: () => { this.display = "horizontal"; }
          }, {
            icon: "view_stream",
            active: this.display == "vertical",
            click: () => { this.display = "vertical"; }
          }],
          menu_width: 55,
          menu_class: "align-right"
        }
      ]
    },

    // Formats management
    current_format_name () {
      const format = this.formats.find(([, width_mm, height_mm]) => (this.page_format_mm[0] == width_mm && this.page_format_mm[1] == height_mm));
      return format ? format[0] : (this.page_format_mm[0]+"mm x "+this.page_format_mm[1]+"mm");
    },
    formats: () => [
      ["A0", 841, 1189],
      ["A0L", 1189, 841],
      ["A1", 594, 841],
      ["A1L", 841, 594],
      ["A2", 420, 594],
      ["A2L", 594, 420],
      ["A3", 297, 420],
      ["A3L", 420, 297],
      ["A4", 210, 297],
      ["A4L", 297, 210],
      ["A5", 148, 210],
      ["A5L", 210, 148],
      ["A6", 105, 148],
      ["A6L", 148, 105]
    ],

    // Margins management
    current_margins_name () {
      const margins = this.margins.find(([, margins]) => (this.page_margins == margins));
      return margins ? margins[0] : this.page_margins;
    },
    margins: () => [
      ["Medium", "20mm"],
      ["Small", "15mm"],
      ["Slim", "10mm 15mm"],
      ["Tiny", "5mm"]
    ],

    // Current text style management
    current_text_style () { return this.mounted ? this.$refs.editor.current_text_style : false; },
    isLeftAligned () { return ["start", "left", "-moz-left"].includes(this.current_text_style.textAlign); },
    isRightAligned () { return ["end", "right", "-moz-right"].includes(this.current_text_style.textAlign); },
    isCentered () { return ["center", "-moz-center"].includes(this.current_text_style.textAlign); },
    isJustified () { return ["justify", "justify-all"].includes(this.current_text_style.textAlign); },
    isBold () {
      const fontWeight = this.current_text_style.fontWeight;
      return fontWeight && (parseInt(fontWeight) > 400 || fontWeight.indexOf("bold") == 0);
    },
    isItalic () { return this.current_text_style.fontStyle == "italic"; },
    isUnderline () { // text-decoration is not overridden by children, so we query the parent stack
      const stack = this.current_text_style.textDecorationStack;
      return stack && stack.some(d => (d.indexOf("underline") == 0));
    },
    isStrikeThrough () { // text-decoration is not overridden by children, so we query the parent stack
      const stack = this.current_text_style.textDecorationStack;
      return stack && stack.some(d => (d.indexOf("line-through") == 0));
    },
    isNumberedList () { return this.current_text_style.isList && this.current_text_style.listStyleType == "decimal"; },
    isBulletedList () { return this.current_text_style.isList && ["disc", "circle"].includes(this.current_text_style.listStyleType); },
    isH1 () { return this.current_text_style.headerLevel == 1; },
    isH2 () { return this.current_text_style.headerLevel == 2; },
    isH3 () { return this.current_text_style.headerLevel == 3; },
    curColor () { return this.current_text_style.color || "transparent"; },

    // Platform management
    isMacLike: () => /(Mac|iPhone|iPod|iPad)/i.test(navigator.platform),

    // Undo / redo flags
    can_undo () { return this.undo_count > 0; },
    can_redo () { return this.content_history.length - this.undo_count - 1 > 0; }
  },

  methods: {
    // Page overlays (headers, footers, page numbers)
    overlay (page, total) {
      // Add page numbers on each page
      let html = '<div style="position: absolute; bottom: 8mm; ' + ((page % 2) ? 'right' : 'left') + ': 10mm">Page ' + page + ' of ' + total + '</div>';

      // Add custom headers and footers from page 3
      if(page >= 3) {
        html += '<div style="position: absolute; left: 0; top: 0; right: 0; padding: 3mm 5mm; background: rgba(200, 220, 240, 0.5)"><strong>MYCOMPANY</strong> example.com /// This is a custom header overlay</div>';
        html += '<div style="position: absolute; left: 10mm; right: 10mm; bottom: 5mm; text-align:center; font-size:10pt">Copyright (c) 2020 Romain Lamothe, MIT License /// This is a custom footer overlay</div>';
      }
      return html;
    },

    // Undo / redo functions examples
    undo () { if(this.can_undo){ this._mute_next_content_watcher = true; this.content = this.content_history[--this.undo_count]; } },
    redo () { if(this.can_redo){ this._mute_next_content_watcher = true; this.content = this.content_history[++this.undo_count]; } },
    resetContentHistory () { this.content_history = []; this.undo_count = -1; },

    // Insert page break function example
    async insertPageBreak () {
      // insert paragraph at caret position
      document.execCommand("insertParagraph");

      // insert a marker at caret position (start of the new paragraph)
      const marker = "###PB###"; // must be regex compatible
      document.execCommand("insertText", false, marker);

      // wait for DOM update
      await this.$nextTick();

      // find the marker inside content items and split this content item in two items between the two paragraphs
      // only match root tags (p, div, h1, h2...) to avoid non-root tags like <li>
      const regexp = new RegExp("<(p|div|h\\d)( [^/>]+)*>(<[^/>]+>)*"+marker);
      for(let i = 0; i < this.content.length; i++) {
        const item = this.content[i];
        if(typeof item != "string") continue;
        const match = regexp.exec(item);
        if(match) {
          const tags_open = match[0].slice(0, -marker.length);
          let content_plus_tags_close = item.substr(match.index + match[0].length);
          // insert <br> to empty pages that would not be handled correctly by contenteditable
          if(content_plus_tags_close.indexOf("</") == 0) content_plus_tags_close = "<br>" + content_plus_tags_close;
          this.content.splice(i, 1, item.substr(0, match.index), tags_open + content_plus_tags_close);
          return;
        }
      }

      // if the code didn't return before, the split didn't work (e.g. inside a <li>). just remove the marker from the content
      for(let i = 0; i < this.content.length; i++) {
        const item = this.content[i];
        if(typeof item != "string" || item.indexOf(marker) < 0) continue;
        this.content.splice(i, 1, item.replace(marker, ''));
        break;
      }
    }
  },

  watch: {
    content: {
      immediate: true,
      // Fill undo / redo history stack on user input
      handler (new_content) {
        if(!this._mute_next_content_watcher) { // only update the stack when content is changed by user input, not undo/redo commands
          this.content_history[++this.undo_count] = new_content;
          this.content_history.length = this.undo_count + 1; // remove all redo items
        }
        this._mute_next_content_watcher = false;
      }
    }
  }
}
</script>

<style>
html {
  height: 100%;
}
body {
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: black;
  background: rgb(248, 249, 250);
}
::-webkit-scrollbar {
  width: 16px;
  height: 16px;
}
::-webkit-scrollbar-track, ::-webkit-scrollbar-corner {
  display: none;
}
::-webkit-scrollbar-thumb {
  background-color: rgba(0, 0, 0, 0.5);
  border: 5px solid transparent;
  border-radius: 16px;
  background-clip: content-box;
}
::-webkit-scrollbar-thumb:hover {
  background-color: rgba(0, 0, 0, 0.8);
}
</style>

<style scoped>
  .main {
    width: fit-content;
    min-width: 100%;
  }
  .bar {
    position: sticky;
    left: 0;
    top: 0;
    width: calc(100vw - 16px);
    z-index: 1000;
    background: rgba(248, 249, 250, 0.8);
    border-bottom: solid 1px rgb(248, 249, 250);
    backdrop-filter: blur(10px);
    --bar-button-active-color: #188038;
    --bar-button-open-color: #188038;
    --bar-button-active-bkg: #e6f4ea;
    --bar-button-open-bkg: #e6f4ea;
  }
</style>