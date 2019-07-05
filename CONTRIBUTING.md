image: docker:stable
services:
  - docker:dind

variables:
  DOCKER_DRIVER: overlay
  SPRING_PROFILES_ACTIVE: gitlab-ci

stages:
  - build

node-build:
  image: nexus-docker.ingosoft.cn/node:umi-taro-angular
  stage: build
  script: 
    - unzip -q node_modules.zip || echo "缓存不存在"
    - npm install
    - npm run build
  artifacts:
    paths:
      - dist/*.*
