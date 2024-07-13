# challenges HelpfulDesk

## Description: 

bài này mới chỉ download được file zip update bị lỗ hổng 

## solve 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/20c05a86-724c-4310-80f3-7c0306452010)

+ bài này ta sẽ download file zip chưa bản update bị lỗ hổng của trang web này

+ unzip file ra ta có rất nhiều file config sau đó ta có thể decomplie file exe bằng cách dùng dotpeek để reverse code

![image](https://github.com/j10nelop/m3d1r/assets/152776722/38198e2a-c615-4dc1-b205-6f9c8e16214c)


+ trong đó ta thấy có 1 dòng code config có 1 thông tin về path ẩn

```
public IActionResult SetupWizard()
    {
      if (File.Exists(this._credsFilePath))
      {
        PathString path = ((ControllerBase) this).HttpContext.Request.Path;
        if (((PathString) ref path).Value.TrimEnd('/').Equals("/Setup/SetupWizard", StringComparison.OrdinalIgnoreCase))
          return (IActionResult) this.View("Error", (object) new ErrorViewModel()
          {
            RequestId = "Server already set up.",
            ExceptionMessage = "Server already set up.",
            StatusCode = 403
          });
      }
      return (IActionResult) this.View();
```

challenge.nahamcon.com:30491/Setup/SetupWizard/

![image](https://github.com/j10nelop/m3d1r/assets/152776722/c29405f1-201d-4899-b238-63c012932364)

+ add thêm username password ta đặt là admin:admin

nhắc lại dotpeek ta check phân helpfuldesk controller 

![image](https://github.com/j10nelop/m3d1r/assets/152776722/baee7517-9d98-499c-b65f-80634bf9260a)


+ sau đăng nhập vào ta được HOST-WIN-DX130S2

![image](https://github.com/j10nelop/m3d1r/assets/152776722/dc277c6d-a05a-4934-9000-016b7ec22bd6)

=> flag: flag{2fd5d91a4504ecf32a1b701a4b7122db}



**trong bài có sử dụng thêm tool snyk.io**
