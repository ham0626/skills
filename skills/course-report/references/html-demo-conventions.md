# 单文件交互 HTML demo 代码范式

供 `course-report` skill 在"阶段 3 · HTML demo 路线"参考。脚手架见 `assets/demo-template/index.html`，本文件提炼可复用的关键范式，避免每次从零重写。

---

## 1. 主题变量（CSS `:root`）

用 CSS 变量集中管理配色，换主题只改这一处：

```css
:root{
  --bg:#050805;            /* 暗黑底 */
  --primary:#6fdc4a;       /* 主题色（如毒性绿） */
  --primary-bright:#9bff7a;
  --glow:rgba(111,220,74,.55);
  --alert:#ff3b3b;         /* 警告红 */
  --text:#e8f5e4;
}
```

- 暗黑汇报优先深色底 + 高对比文字；IP 梗（生化危机）用绿/红，避免橙色除非用户指定。
- 需要亮色背景时反转 `--bg` 与 `--text` 即可。

## 2. 分屏导航（多 section 一页一屏）

```html
<section class="slide" data-i="0">…</section>
<section class="slide" data-i="1">…</section>
```
- JS 维护 `current`，`→` / `空格` / 点击左右区翻页；禁用"点屏幕任意处翻页"以免与节点点击冲突。
- 每个 section 用 `.slide-inner` 居中内容，留安全边距。

## 3. SVG 事故树 + 点击弹题（核心交互）

- 事故树用内联 `<svg>` 画节点 + 连线（矩形=事件，菱形=逻辑门）。
- 每个可点节点加 `data-node="n1"`，监听 click → `openModal(id)`。
- 弹窗 = 固定定位的 div，含"这个环节发生了什么 + 一个问题"，点击遮罩关闭。

```js
function openModal(id){
  const data={n1:["环节标题","当时发生了什么…","抛给观众的问题：…"]};
  // 填充标题/正文/问题，显示 modal
}
document.querySelectorAll('[data-node]').forEach(el=>{
  el.addEventListener('click',()=>openModal(el.dataset.node));
});
```

**关键**：问题写在弹窗里，不要另起一页逐个展开；不要做"右侧静态列全部因素"，会显得又是横向。

## 4. 瑞士奶酪动画（对齐 + 闪烁警告）

- 几片半透明"带孔"矩形（用 `radial-gradient` 或多个圆孔 div）水平错位排列。
- JS 或 CSS `transition` 让它们 `translateX` 对齐；对齐后某个 ⚠ 元素加 `.blink`（CSS `@keyframes` 改 opacity）闪烁。
- 触发时机：进入该 section 时播放一次。

## 5. 灯箱放大（画廊只放大报告图）

```css
.lightbox{position:fixed;inset:0;background:rgba(0,0,0,.93);display:none;…z-index:300}
.lightbox.show{display:flex}
.gitem img{cursor:zoom-in}
```
```js
document.querySelectorAll('.gitem img').forEach(im=>{
  im.addEventListener('click',()=>{
    document.getElementById('lbimg').src=im.src;
    document.getElementById('lbcap').textContent=im.alt||'';
    document.getElementById('lightbox').classList.add('show');
  });
});
// 点击灯箱本身关闭
```

**只给画廊图片绑 lightbox**，避免误放大装饰图。

## 6. 灰度底图保证可读性（谢谢页 / 封面）

底图用 `filter:grayscale(1) brightness(.4)` + 一层 `linear-gradient` 暗化遮罩，确保文字清晰：

```css
.thanks-bg{position:absolute;inset:0;background:url('assets/xxx.png') center/cover;filter:grayscale(1) brightness(.40);opacity:.6}
.thanks-scrim{position:absolute;inset:0;background:linear-gradient(180deg,rgba(5,8,5,.85),rgba(5,8,5,.92))}
```

## 7. 去专业化 + 来源标注

- 把 `1% NP40+PBS+1% SDS 冰浴60min` 这类专业串 → "未经验证的灭活方法"；`HT-SCoV-2` → "实验室正在使用的那株病毒"，但保留"全基因组高度同源"等权威表述。
- 真实事件 / 法规 / 报告在页面底部或备注标注出处（卫健委摘要、国务院令 424 号）。

## 8. 容灾

- 每次关键改动后保留 `index.html.bak`。
- 图片放 `assets/`，用相对路径引用，确保发布后（`workbuddy_sites_deploy` 静态托管）能加载。
