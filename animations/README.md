# 自定义 Logo 动效 / Custom Logo Animation

把做好的动效文件丢进这个文件夹，告诉我文件路径，我就接上。

Two recommended formats — pick whichever tool you use:

## Option A — Lottie JSON (recommended)

如果你用 **After Effects + Bodymovin**、**Rive**、**Figma + LottieFiles**、或 **Jitter**，导出一个 Lottie JSON 文件：

```
big-cad-logo.json
```

**为什么 Lottie**：
- 矢量、可任意缩放不变糊
- 文件小（典型 20-200KB）
- 支持图层、loop、复杂时间轴
- 我只需要 `lottie-web` 包，几行代码接进去

**导出建议**：
- After Effects：Bodymovin 插件 → 选 "Glyphs" 或 "Shapes" 保留矢量
- Rive：导出 .riv 文件（也支持，需要 `rive-react` 包，但体积大些）
- Figma：LottieFiles 插件 → File → Export → Lottie JSON

---

## Option B — 带 CSS keyframes 的 SVG

如果你用 **Figma / Illustrator** 画一帧帧 SVG，或用纯 CSS 写：

```
big-cad-logo.svg
```

**约束**：
- 文件放在这个文件夹，加 `<style>` 标签内部写 `@keyframes`
- 用 `currentColor` 继承文字色（品牌奶白）

**示例骨架**：
```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 200">
  <style>
    /* fill 灌入 */
    .stroke-only { fill: transparent; stroke: currentColor; stroke-width: 4; }
    .fillable { animation: fill-in 1s 1.4s forwards; }
    @keyframes fill-in { to { fill: currentColor; stroke-width: 0; } }
    /* 或者笔画逐画 */
    .draw { stroke-dasharray: 500; stroke-dashoffset: 500; animation: draw 1.5s forwards; }
    @keyframes draw { to { stroke-dashoffset: 0; } }
  </style>
  <path class="stroke-only draw fillable" d="..."/>
</svg>
```

---

## 我会做的 / What I'll do

1. 在 `components/AnimatedLogo.tsx` 写适配组件，按你给的文件名走对应分支
2. Hero.tsx 换成 `<AnimatedLogo />`
3. TopNav 左上角的小 logo 也换成 AnimatedLogo（保持一致）
4. 加 `lottie-web` 依赖（Lottie 情况）

## 不推荐

- ❌ MP4：加载慢、不能缩放、要解压
- ❌ GIF：体积大、画质差、不能交互
- ❌ WebGL / Three.js：杀鸡用牛刀，bundle 加 100KB+

做好了告诉我文件名（+ 如果是 Lottie，要不要循环 / 触发时机），我接上去。
