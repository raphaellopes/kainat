# Base Apache + PHP + MySQL docker

This project was created to help with to work with [Bedrock](https://roots.io/bedrock/).
You create and run php, mysql and apache containers to serve your app.

## Prerequisites
- [Docker](https://www.docker.com/)

## Usage

Clone this repo and folow the commands bellow start to work on your 
local environment:

```
# clone the project
git clone git@bitbucket.org:Raphaellopes07/wp-base-docker.git

# go to app folder
cd wp-base-docker/app/

# copy the `.env.example` to `.env` and change the env vars
cp .env.example .env

# build and run the baseic containers `make -C <container> <task>`
make -C php-fmp build run
make -C apache build run
make -C mysql run
```

## Help
```
make -C <container> help
```
