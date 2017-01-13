# webpack细节tips整理：

1.关于devserver:
	配置项
		contentBase: 'http://localhost/', //基本路径
		hot: 'true', //热插拔
		historyApiFallback: false,  //html5模式的history  =>
		对应nginx配置如下：
		> 
			location / { 
			  expires -1; add_header Pragma "no-cache"; 
			  add_header Cache-Control "no-store, no-cache, must-revalidate, post-check=0, pre-check=0";
			 root /var/web;
			 try_files $uri $uri/ /index.html =404; 
			}
		// 这一块暂时不是很懂，一会理解下。
		compress: 'true', //压缩assets,
		proxy: {
			'/some/path*' : {
				target: 'https://other-server.example.com',
				secure: false,
				changeOrigin: true
			}
		},
		headers: {
            "Access-Control-Allow-Origin": "*",
        },

    webpackDevServer(compiler,config).listen(port);
    
	@https://webpack.github.io/docs/webpack-dev-server.html;
2. 关于string-replace-loader:
	e.g:
	loaders: [
      {
        test: /\.js$/,
        loader: 'string-replace',
        query: {
          multiple: [
             { search: 'jQuery', replace: 'window.$' },
             { search: '_', replace: 'window.lodash', flags: 'g'}
          ]
        }
      }
    ]


