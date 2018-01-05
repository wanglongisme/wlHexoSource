---
layout: post
title: jquery的ajax上传文件
comments: false
categories:
  - 随笔
tags:
  - 2016
abbrlink: 2f36df26
date: 2016-12-26 13:38:57
---

做这个blog的时候需要使用ajax上传文件,费了点功夫, 记录下来.
html:
```html
<form id=”my_form” target=”form_target” method=”post” enctype=”multipart/form-data” style=”width:0px;height:0;overflow:hidden”>
<input id=”file_input” name=”file” type=”file” onchange=”uploadImg();”>
</form>
```
js:
```javascript
function uploadImg() {
    var formData = new FormData();
    formData.append(“file”, $(“#file_input”)[0].files[0]);
    $.ajax({
        url: “upload / img.php”,
        type: “POST”,
        data: formData,
        dataType: “text”,
        //告诉jQuery不要去处理发送的数据
        processData: false,
        //阻止jquery修改contentType报表头,导致传输文件的边界无法识别的错误.
        contentType: false,
        success: function(imgUrl) {
            console.log(imgUrl);
            $(inputId).val(imgUrl);
        },
        error: function(data) {
            console.log(“upload - img - error: “ + JSON.stringify(data));
        }
    });
}
```

java:

```java
@ResponseBody
 @RequestMapping(value="/upload/img", method=RequestMethod.POST)
 public String uploadImg(MultipartFile file,HttpServletRequest request) throws Exception{
 String returnUrl = "";
 if (file!=null) {// 判断上传的文件是否为空
 String path=null;// 文件路径
 String type=null;// 文件类型
 String fileName=file.getOriginalFilename();// 文件原名称
 System.out.println("上传的文件原名称:"+fileName);
 // 判断文件类型
 type=fileName.indexOf(".")!=-1?fileName.substring(fileName.lastIndexOf(".")+1, fileName.length()):null;
 if (type!=null) {// 判断文件类型是否为空
 if ("GIF".equals(type.toUpperCase())||"PNG".equals(type.toUpperCase())||"JPG".equals(type.toUpperCase())) {
 // 项目在容器中实际发布运行的根路径
 String realPath=request.getSession().getServletContext().getRealPath("/");
 // 自定义的文件名称
 String trueFileName=String.valueOf(System.currentTimeMillis())+fileName;
 returnUrl = trueFileName;
 // 设置存放图片文件的路径
 path=realPath+"upload"+File.separator+"image"+File.separator+trueFileName;
 //System.out.println("存放图片文件的路径:"+path);
 // 转存文件到指定的路径
 try {
 file.transferTo(new File(path));
 } catch (Exception e) {
 // TODO Auto-generated catch block
 e.printStackTrace();
 }
 returnUrl = trueFileName;
 //System.out.println("文件成功上传到指定目录下");
 }else {
 System.out.println("不是我们想要的文件类型,请按要求重新上传");
 }
 }else {
 System.out.println("文件类型为空");
 }
 }else {
 System.out.println("没有找到相对应的文件");
 }
 System.out.println("返回图片路径: upload"+File.separator+"image"+File.separator+returnUrl);
 return "upload"+File.separator+"image"+File.separator+returnUrl;
 }

```

