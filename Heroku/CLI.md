### CLI Usage
```shell
# Login
> heroku login

# Using an Http Proxy
# For Unix
$ EXPORT HTTP_PROXY=http://proxy.server:port
or
$ EXPORT HTTPS_PROXY=http://proxy.server:port
$ heroku login

# For Windows
> set HTTP_PROXY=http://proxy.server:port
or
> set HTTPS_PROXY=http://proxy.server:port
> heroku login

# Prepare the app
> git clone https://github.com/heroku/node-js-getting-started.git
> cd node-js-getting-started

# Create an app
> heroku create

# Clone the repository
> heroku git:clone -a mighty-plains-51050

# Deploy the changes
> git add .
> git commit -am "your comment"
> git push heroku master
```


