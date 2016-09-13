#HTML5图片文件上传(含拖拽、预览、上传、美化)

##关于接口

>File API

* File - 独立文件;提供只读信息,例如名称、文件大小、mimetype和对文件句柄的引用。

* FileList - File 对象的类数组序列(考虑多文件上传或者从桌面拖动目录或文件)

* Blob - 可将文件分割为字节范围

* FileReader - 读取File或者Blob

* URL scheme

##检测浏览器是否支持

<code>

if(window.File && window.FileReader && window.FileList && window.Blob){
    //ok
}else{
    alert('不支持处理');
}
</code>

>基本代码

<code>
(function(window,$){
            $(document).on('change','#img_input',function(e){
                //获取图片资源
                var file = e.target.files[0];
                //过滤其他文件
                if(!file.type.match('image.*')){
                    return false;
                }

                var reader = new FileReader();
                //读取文件
                reader.readAsDataURL(file);
                //渲染文件
                reader.onload = function(arg){
                    var img = '<img class="preview" src="'+arg.target.result+'" alt="preview" />';
                    $(".preview").empty().append(img);
                }
            });
            
})(window,jQuery);
</code>

>上传到服务器代码

<code>
//上传到服务器
var form_data = new FormData();
var file_data = $("#img_input").prop("files")[0];

//把上传的数据放入到form_data
form_data.append('user','JV');
form_data.append('img',file_data);

$.ajax({
    type:"POST",
    url:"./upload.php",
    dataType:'json',
    processData:false,
    contentType:false,
    data:form_data
}).success(function(ret){
    console.log(ret);
}).fail(function(ret){
    console.log(ret);
});
</code>

##拖拽上传

* dragenter

* dragover

* drop

>关键代码

<code>
(function(window,jquery){
            //拖拽文件上传 
            
            //必须组织dragenter和dragover事件的默认行为 这样才能触发drop事件
            function fileSelect(evt){
                evt.stopPropagation();
                evt.preventDefault();
                //文件对象
                var files = evt.dataTransfer.files;

                //处理文件
                for(var i=0,f; f= files[i];i++){
                        var reader = new FileReader();
                        //读取文件
                        reader.readAsDataURL(f);
                        //渲染文件
                        reader.onload = function(arg){
                            var img = '<img class="preview" src="'+arg.target.result+'" alt="preview" />';
                            $("#drop_zone").empty().append(img);
                        }
                }
            }

            function dragOver(evt){
                evt.stopPropagation();
                evt.preventDefault();
                evt.dataTransfer.dropEffect = 'copy';
            }

            var dropZone = document.getElementById('drop_zone');
            dropZone.addEventListener('dragover',dragOver,false);
            dropZone.addEventListener('drop',fileSelect,false);
            /*$("#drop_zone").on('dragover', function(e){
                e.stopPropagation();
                e.preventDefault();
                handleDragOver(e.originalEvent);
            });

            $("#drop_zone").on('drop', function(e){
                e.stopPropagation();
                e.preventDefault();
                handleFileSelect(e.originalEvent);
            });*/
        })(window,jQuery);
</code>
