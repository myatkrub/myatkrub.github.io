---
title: Sweet Alert ကို User Event Script မှာအသုံးပြုခြင်း
date: "2020-03-14T22:12:03.284Z"
description: "Sweet Alert ကို User Event Script မှာအသုံးပြုခြင်း"
---
![](./alert.png)

**Sweet Alert JS** အား NetSuite User Event Script မှာအသုံးပြုချင်ရင် အောက်ပါ Code အားအသုံးပြုစမ်းသပ်နိုင်ပါသည်။ 

Sweet Alert Script
```javascript
swal("Hello Myatkrub!")
```
---
UserEvent Script
```javascript
function beforeLoad(type, form, request) {
    if (type == 'create') {
        var sweet = '';
        sweet += '<html><body><script src="https://unpkg.com/sweetalert/dist/sweetalert.min.js"></script><script type=\'text/javascript\'>swal("Hello Myatkrub!")</script></body></html>';
        var field = form.addField("custpage_alertfield", "inlinehtml");
        field.setDefaultValue(sweet);
    }
}

```

တခြား alert, pup up များကို

 https://sweetalert.js.org/  တွင်သွားရောက် လေ့လာနိုင်ပါကြောင်း... 






