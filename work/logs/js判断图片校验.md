## js进行图片的校验 



    var ImgObj=new Image();
    ImgObj.src= 'url';
    
    if(ImgObj.fileSize > 0 || (ImgObj.width > 0 && ImgObj.height > 0))
    {
    console.log('有效');
    } else {
    console.log('无效');
    }


