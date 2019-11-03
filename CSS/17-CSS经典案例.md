### 画三角形

```css
#top-triangle {
  width: 0;
  height: 0;
  border-bottom: 100px solid red;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
}

#bottom-triangle {
  width: 0;
  height: 0;
  border-left: 50px solid transparent;
  border-right: 50px solid transparent;
  border-top: 100px solid blue;
}

#left-triangle {
  width: 0;
  height: 0;
  border-top: 50px solid transparent;
  border-bottom: 50px solid transparent;
  border-right: 100px solid orange;
}

#right-triangle {
  width: 0;
  height: 0;
  border-top: 50px solid transparent;
  border-bottom: 50px solid transparent;
  border-left: 86px solid greenyellow;
}
```

--------------------------------------

### 画一条0.5px宽的线

```css
#line {
  width: 100px;
  height: 1px;
  background-color: red;
  transform: scaleY(0.5);
}
```