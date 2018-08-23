# DemoBook

[![Travis (.org)](https://img.shields.io/travis/hiroppy/demobook.svg?style=flat-square)](https://travis-ci.org/hiroppy/demobook)

DemoBook will automatically deploy static files to your hosted server and generate appropriate URLs.  
For example, it is possible to support a review of PR by making CI execute CLI.  
Also, the bot can also post the URL as a comment from a server.

## Packages

- cli
  - `npm i @demobook/cli`
- server

## Sample

![](media/comment.png)

Currently, this repository is running demobook-cli when running CI of Travis.  
see: https://travis-ci.org/hiroppy/demobook

```yml
# travis.yml
sudo: false
language: node_js
cache:
  directories:
    - node_modules
node_js:
  - 10
os:
  - linux
before_script:
  - npm i
  - npm run cat
  - npx @demobook/cli -o hiroppy -r demobook -t https://demobook-ci.herokuapp.com -d output --pr ${TRAVIS_PULL_REQUEST} -n cat
  - npm run dog
  - npx @demobook/cli -o hiroppy -r demobook -t https://demobook-ci.herokuapp.com -d build --pr ${TRAVIS_PULL_REQUEST} -n dog
```

After that, it is uploading a static file to Heroku.

As you can see, CLI is output an URL of Heroku. This URL is random.

If you want Bot to comment on PR of GitHub which it is deployed, it is possible to enter username and password on the demobook/server.

see: [.env](/packages/server/.env.sample)
