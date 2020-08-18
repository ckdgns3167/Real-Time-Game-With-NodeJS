## 프로젝트 세팅

1. <u>**babel 세팅**</u>

   - src 폴더 생성

   - yarn init 입력: package.json 생성

   - yarn add nodemon 

   - yarn add express 

   - yarn add socket.io 

   - src 폴더 안에 server.js 생성

     ```javascript
     import express from "express"
     ```

   - yarn add @babel/node

   - yarn add @babel/core

   - yarn add @babel/preset-env

   - package.json 파일에 scripts 작성

     ```json
     ...
       "express": "^4.17.1",
         "nodemon": "^2.0.4",
         "socket.io": "^2.3.0"
       },
       "scripts": {
         "dev:server": "nodemon --exec babel-node src/server"
       }
     }
     ```

   - .babelrc 파일 생성

     ```babel
     {
         "presets": [
             "@babel/preset-env"
         ]
     }
     ```
     
   - yarn dev:server
   
2. **<u>서버 세팅</u>**

   - pug 설치(yarn add pug) 후 server.js 

     ```javascript
     import express from "express";
     
     const PORT = 4000;
     const app = express();
     app.set("views engine", "pug");
     
     const handleListening = () =>
         console.log(`✅ Server running: http://localhost:${PORT}`);
     
     app.listen(PORT, handleListening);
     ```

   - src에 views와 static 폴더 생성

   - views에 home.pug 생성 후 html:5 입력하여 코드 생성

     ```pug
     <!DOCTYPE html>
     html(lang="en")
         head
             meta(charset="UTF-8")
             meta(name="viewport", content="width=device-width, initial-scale=1.0")
             title Guess Mine
         body 
             h1 Hello
     ```

   - static에 index.js 생성

   - 다시 server.js에 코드 추가

     ```javascript
     import { join } from "path";
     import express from "express";
     import socketIO from "socket.io";
     
     const PORT = 4000;
     const app = express();
     app.set("view engine", "pug");
     app.set("views", join(__dirname, "views"));
     app.use(express.static(join(__dirname, "static")));
     app.get("/", (req, res) => res.render("home"));
     
     const handleListening = () =>
         console.log(`✅ Server running: http://localhost:${PORT}`);
     
     app.listen(PORT, handleListening);
     ```

3. **<u>ESLint 세팅</u>**

   - yarn add eslint-config-prettier -D
   - yarn add eslint-plugin-prettier -D
   - yarn add prettier -D

4. **<u>SocketIO 세팅</u>**

   - express 포트와 같은 포트에서 작업할 것이다. traffic이 다르기 때문에 가능하다. ws와 http는 동시에 같은 서버에서 존재할 수 있다.

   - SocketIO는 서버와 클라이언트가 동시에 될 수 있다.

   - socket.io/socket.io.js 는 기본적으로 프런트엔드 코드인데 백엔드와 프런트엔드가 서로 대화할 수 있게 해주는 코드이다.

   - server.js 추가 코드

     ```javascript
     ...
     const server = app.listen(PORT, handleListening);
     
     const io = socketIO(server);
     ```

5. 기본 세팅 끝.

