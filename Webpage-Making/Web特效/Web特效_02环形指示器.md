# Web特效_02环形指示器

基本属性设置

```javascript
$(function () {
    radialIndicator("#app",{
        initValue: 50,
        radius: 100,
        barWidth:20,
        barColor:"#ff0000",
        roundCorner:true,
        minValue:0,
        maxValue:60,
        //    minval和maxval控制取值范围，初始值在该取值范围中根据占比确定初始的值
    })
})
```

