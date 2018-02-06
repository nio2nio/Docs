### Login
```shell
heroku login
```

### Using an Http Proxy
  * For Unix
  ```shell
  EXPORT HTTP_PROXY=http://proxy.server:port
  EXPORT HTTPS_PROXY=http://proxy.server:port
  ```
  * For Windows
  ```shell
  set HTTP_PROXY=http://proxy.server:port
  set HTTPS_PROXY=http://proxy.server:port
  ```

### Prepare the app
  ```shell
  git clone https://github.com/heroku/node-js-getting-started.git
  cd node-js-getting-started
  ```

### Create an app
  ```shell
  heroku create
  ```

### Clone the repository
  ```shell
  heroku git:clone -a mighty-plains-51050
  ```
  
### Deploy the changes
  ```shell
  git add .
  git commit -am "your comment"
  git push heroku master
  ```


