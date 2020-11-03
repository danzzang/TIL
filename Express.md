# node.js + Express

## 1. node.js

> 브라우저가 아닌 환경에서도 자바스크립트를 사용할 수 있게 하는 자바스크립트 런타임
>
> - node.js는 웹 서버가 아니다. 
> - 웹 서버는 html 파일 경로를 지정해주고, 서버를 열고, 세션 이런것도 관리해주는데  node.js는 http 서버를 직접 작성해야 한다
> - 그저 코드를 실행할 수 있는 하나의 방법에 불과하는 자바스크립트 런타임 일 뿐 



## 2. Express

> 웹 서버에서 필요한 대부분의 기능이 이미 구현된 웹 프레임 워크
>
> 라우팅, 세션, 템플릿 등 웹 어플리케이션을 만들면서 필요한 기능 이미 구현됨



#### 1. Express 설치

```bash
npm install -g express-generator
npm install express
```



#### 2. Express 프로젝트 생성

```bash
express TamTam(프로젝트명)
cd TamTam
npm install

# run app
$ DEBUG=tamtam:* npm start
```



#### 3. model

```js
// mongodb
const mongoose = require('mongoose')
const Schema = mongoose.Schema

const companySchema = new mongoose.Schema({
	company_id: {
		type: Number,
		allowNull: false,
		autoIncrement: true,
		primaryKey: true,
	},
	company_email: {
		type: String,
		allowNull: false,
		unique: true,
	},
	company_nickname: {
		type: String,
		allowNull: false,
		unique: true,
	},
	company_pwd: {
		type: String,
		allowNull: false,
	},
	company_industry: {
		type: String,
		allowNull: false,
	}
})

const companyModel = mongoose.model("company", companySchema)

module.exports = companyModel;
```



#### 4. routes

```js
// library
const express = require('express')
const crypto = require("crypto")
const jwt = require("jsonwebtoken")
const secretObj = require("../config/jwt")

// Model
const companyModel = require('../models/companyModel')

// Routes 
const companyRoutes = express.Router()

// 함수
const hashpassword = (password) => {
	return crypto.createHash("sha512").update(password).digest("hex")
}

// API
companyRoutes.get('/', async (req, res) => {
	console.log('접근완료')
})

// 회원가입
companyRoutes.post('/signup', async (req, res) => {
	try {
		const companyEmail = req.body.company_email
		const companyPwd = req.body.company_pwd
		const companyNick = req.body.company_nickname
		const companyIndustry = req.body.company_industry

		const item = new companyModel({
			company_email: companyEmail,
			company_pwd: hashpassword(companyPwd),
			company_nickname: companyNick,
			company_industry: companyIndustry, 
		})
		await item.save()
		res.status(200).send({
			message: `${companyEmail} 회원가입이 완료되었습니다.`
		})
	} catch(err) {
		res.status(500).send(err)
	}
})

// 로그인
companyRoutes.post('/login', async (req, res) => {
	if (req.headers.token){
		res.status(403).json({ message: "이미 로그인 되어있습니다." })
	} else {
		const companyEmail = req.body.company_email
		const companyPwd = hashpassword(req.body.company_pwd)

		await companyModel.findOne({ company_email: companyEmail })
			.then((company) => {
				if (company.company_pwd !== companyPwd) {
					res.status(403).send({ message: "비밀번호가 다릅니다." })
				} else {
					console.log(secretObj)
					jwt.sign(
						{ company_email: company.company_email },
						secretObj.secret,
						{ expiresIn: '1d' },

						function (err, token) {
							if (err) {
								res.send(err)
							} else {
								res.json({
									message: "로그인 성공, 토큰을 발급합니다.",
									token: token,
									status: "login",
									company_email: company.company_email,
								})
							}
						}
					)
				}
			})
			.catch((err) => {
				res.status(403).send({
					message: "존재하지 않는 아이디입니다."
				})
			})
	}
})

// 회원탈퇴
companyRoutes.delete("/", async (req, res) => {
	try {
		await companyModel.findOne({ company_email: req.headers.company_email})
		.then(async (company) => {
			if (company === null) {
				res.status(403).send({ message: "존재하지 않는 아이디 입니다."})
			} else {
				// 다른 모델에서도 회원 정보를 지워줘야 한다. 
				await companyModel.deleteOne({ company_email: company.company_email })
				res.status(200).send({ message: "회원 탈퇴 되었습니다."})
			}
		})
	} catch (err) {
		res.status(500).send(err)
	}
})

module.exports = companyRoutes;
```



#### 5. app.js

```js
const express = require('express')
const cors = require('cors')

const companyRoutes = require("./routes/companyRoutes")

const app = express()
app.use(cors())
app.use(express.json())

// routes
app.use("/api/company", companyRoutes)

// model
require("./models/companyModel")

module.exports = app;
```



#### 6. mongodb 연결

```bash
npm install mongoose
```

```js
const app = require('./app')
const http = require('http')
const mongoose = require('mongoose')

const PORT = 3000

const MONGO_URL = "mongodb://localhost:27017/test"
const server = http.createServer(app)
server.listen(PORT)

server.on("listening", async () => {
	console.info(`Listening on port ${PORT}`)

	mongoose.connect(MONGO_URL, {
		useNewUrlParser: true,
		useFindAndModify: false,
		useUnifiedTopology: true,
		useCreateIndex: true,
	})
	mongoose.connection.on("open", () => {
		console.info("Connection to Mongo")
	})
	mongoose.connection.on("error", (err) => {
		console.error(err)
	})
})
```



#### 7. start 정하기

```bash
npm install nodemon 
```

```js
// package.json

// npm start 하면 nodemon으로 server.js 실행 
"scripts": {
	"start": "nodemon server.js"
},
```



## 8. populate 

#### 1. company_model 외래키 설정

```js
const companySchema = new mongoose.Schema({
  company_email: {
    type: String,
    allowNull: false,
    unique: true
  },
  company_nickname: {
    type: String,
    allowNull: false,
    unique: true
  },
  company_pwd: {
    type: String,
    allowNull: false
  },
  company_industry: {
    type: String,
    allowNull: false
  },
  company_execption: [
    {
      type: Schema.Types.ObjectId,
      ref: 'video'
    }
  ],
  company_video: [
    {
      type: Schema.Types.ObjectId,
      ref: 'video'
    }
  ],
  company_channel: [
    {
      type: Schema.Types.ObjectId,
      ref: 'channel'
    }
  ],
  company_contact: [
    {
      type: Schema.Types.ObjectId,
      ref: 'channel'
    }
  ]
})
```



#### 2. 외래키를 이용하여 populate

```js
// 스크랩 채널 조회
companyRoutes.get('/channel', async (req, res) => {
  try {
    const company = await CompanyModel.findOne({
      _id: req.headers.company_id
    }).populate('company_channel')
    res.status(200).send(company)
  } catch (err) {
    res.status(500).send(err)
  }
})
```

