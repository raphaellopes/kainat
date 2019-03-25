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

### Alias
Add this project on your `.bashrc` file (optional)
```
# change path-to-the-project with the path where you cloned this repo
export PATH="$PATH:{path-to-the-project}/bin"
```

Close you terminal and open it again. Now you have an alias called
`wpbase`. You can build your environment running the commands bellow:

```
# build mysql, apache and php images
wpbase build

# run the images with a `.env` file passed as a second arg (see `.env.example` file)
wpbase {path-to-envfile} run
```


## Help
```
make -C <container> help
```
