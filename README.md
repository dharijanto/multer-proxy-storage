# Multer Proxy Storage

This is a custom multer storage engine that proxy the received file into a remote server.
The proxy is forwarded as multipart/form-data.

## Install

```
npm install --save multer-proxy-storage
```

## Usage

In this example we are forwarding user uploaded file into remote server http://www.example.com/upload, with the file
identified with the parameter 'file'.

``` javascript
var multer = require('multer')
var MulterProxyStorage = require('multer-proxy-storage')

this.routePost('/uploadFile',
	(req, res, next) => {
		multer({
			storage: MulterProxyStorage(
				{
					serverPath: `http://www.example.com/upload`,
					fileParamName: 'file'
				}),
			preservePath: true
		}).array('file')(req, res, next)
	}, (req, res, next) => {
		res.send('Success!')
	})

## License
Multer-Proxy-Storage is released under the [MIT](License) license.
