# heroku-buildpack-roswell

This is a generalized [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpacks) for Common Lisp apps using [Roswell](https://github.com/roswell/roswell).

Original work by gos-k: [heroku-bulidpack-roswell](https://github.com/gos-k/heroku-buildpack-roswell). Inspired by José Santos: [heroku-buildpack-cl](https://github.com/jsmpereira/heroku-buildpack-cl).

# Using Buildpack

```
# Create a new Heroku app
heroku create --buildpack https://github.com/anschwa/heroku-buildpack-roswell.git --app <your-app>

# Create Git Repository and add to Heroku
git init && heroku git:remote --app <your-app>

# Implementation choice via environment variables. (any implementation supported by roswell)
heroku config:add ROS_USE={sbcl-bin|ccl|clisp} --app <your-app>

# Install special packages like Clack
heroku config:add ROS_INSTALL=clack --app <your-app>

# To avoid trouble with SBCL source encoding use:
heroku config:add LANG=en_US.UTF-8 --app <your-app>

# Add Postgres Database
heroku addons:create heroku-postgresql:hobby-dev --app <your-app>

# Deploy
git push heroku master

# View App
heroku open
```

# Example Clack App
```
# app.lisp
(lambda (env)
  (declare (ignore env))
  '(200 (:content-type "text/plain") ("Hello, Clack!")))
```

```
# Procfile
web: clackup --port $PORT app.lisp
```

# References
- [Heroku Buildpack API](https://devcenter.heroku.com/articles/buildpack-api#example-buildpacks)