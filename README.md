# 07.10.22
const http = require('http')
const express = require('express')
const app = express()
const handlebars = require('express-handlebars')

const host = '127.0.0.1'
const port = 7000

function notFound(res) {
  res.statusCode = 404
  res.setHeader('Content-Type', 'text/plain')
  res.end('Not found\n')
}

app.engine(
    'handlebars',
    handlebars.engine({ defaultLayout: 'main' })
  )
app.set('views', './views')
app.set('view engine', 'handlebars')

app.get('/', (req, res) => {
    res.render('home', { title: 'Greetings form Handlebars' })
  })
  
  app.listen(port, host, function () {
    console.log(`Server listens http://${host}:${port}`)
  })
  
app.use(express.static(`${__dirname}/assets`));

const server = http.createServer((req, res) => {
  switch (req.method) {
    case 'GET': {
      switch (req.url) {
        case '/home': {
          res.statusCode = 200
          res.setHeader('Content-Type', 'text/plain')
          res.end('Home page\n')
          break
        }
        case '/about': {
          res.statusCode = 200
          res.setHeader('Content-Type', 'text/plain')
          res.end('About page\n')
          break
        }
        default: {
          notFound(res)
          break
        }
      }

      break
    }
    case 'POST': {
      switch (req.url) {
        case '/api/admin': {
          res.statusCode = 200
          res.setHeader('Content-Type', 'text/plain')
          res.end('Create admin request\n')
          break
        }
        case '/api/user': {
          res.statusCode = 200
          res.setHeader('Content-Type', 'text/plain')
          res.end('Create user request\n')
          break
        }
        default: {
          notFound(res)
          break
        }
      }

      break
    }
    default: {
      notFound(res)
      break
    }
  }
})

server.listen(port, host, () => {
  console.log(`Server listens http://${host}:${port}`)
})
