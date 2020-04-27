---
title: "#03. Playing with CSS Variables and JS"
category: Javascript30
---

## 1. HTML
### 1.1 input:color
`type="color"`인 `input`태그가 있다는 걸 처음 알았다. 충격적.


## 2. CSS
### 2.1 :root 선택자와 그 아래 속성들 
```css
:root {
    --base: #ffc600;
    --spacing: 10px;
    --blur: 10px;
}
```


### 2.2 var()
더 충격적.

```css
img{
    padding: var(--spacing);
    background: var(--base);
    filter: blur(var(--blur));
}
```
