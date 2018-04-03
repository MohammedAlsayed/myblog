---
title: "كيف تجعل مدونتك تدعم right-to-left html"
date: 2018-04-03T07:31:53+03:00
draft: false
rtl: true
---


سأقوم بتعديلات في الملفات الأصلية وذلك غير محبذ بشكل عام في عالم البرمجة.

## أولا: 

افتح:
myblog/archetypes/default.md

```
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
---
```
سنقوم بتغييره وذلك بإضافة `rtl: true`

```
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
+ rtl: true
---
```

# ثانيا 
للتغيير اتجاه الصفحة من اليمين لليسار عند وضع `rtl: true`
وبقائها من اليسار لليمين عند وضع `rtl: false`

افتح 
myblog/layouts/partials/post_content.html

قم بإضافة:

```
+ {{if .Params.rtl}}
+    <div dir="rtl" class="post">
-    <div class="post">
        <h1>{{ .Title }}</h1>
        {{ if ne .Params.showpagemeta false }}
...
...
...
  
        {{ end }}
        {{ .Content }}
    </div>
+ {{else}}
// copy and paste the hole <div class="post"> block 
// NOTE: this div does not have rtl attribute
  <div class="post">
    <h1>{{ .Title }}</h1>
    {{ if ne .Params.showpagemeta false }}
    <div class="col-sm-12 col-md-12">
        <span class="text-left post-date meta">

...
...
...

    {{ end }}
    {{ .Content }}
 </div>

+{{ end }}
```

# ثالثا
سنقوم بتعديل ال code block css حتى يكون من اليسار لليمين دائمًا٬ 

سنقوم بإضافة 

```
+    direction: ltr;
``` 

في الملف التالي:
myblog/static/css/custom.css


```
 .hljs {
+    direction: ltr;
     white-space: pre;
     overflow-x: auto; /* no line wrapping */
 }
```

والآن مدونتك جاهزة للكتابة بالعربي !
