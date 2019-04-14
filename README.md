# rails-template

## Description
Simple rails template for general project.

## Requirements
* Rails 6.0.x
* PostgreSQL

## Installation

To generate a Rails application using this template, pass the `-m` option to `rails new`, like this:

```bash
rails new project -T -d postgresql \
    -m https://raw.githubusercontent.com/astrocket/rails-template/master/template.rb
```

*Remember that options must go after the name of the application.* The only database supported by this template is `postgresql`.

## What's included?

* Docker for production deploy
* Nginx Proxy server configuration with Let's encrypt SSL Certificate
* Webpacker and Stimulus setting for client javascript
* ActiveJob + Sidekiq + Redis setting for async jobs 
* Foreman setting for integrative dev setup
* Rspec + FactoryBot setting for test code
* Guard + LiveReload setting for hot reloading

## Foreman start task

Procfile-based applications

with `rails hot`

It runs

* rails
* webpacker
* guard
* sidekiq

## Stimulus generator

Stimulus specific generator task.

with `rails g stimulus posts index`

It generates

* `app/javascript/posts/index_controller.js` with sample html markup containing stimulus path helper.

## Production deploy process

After installing docker & docker-compose in your host machine.

Set up a seperate Nginx-Proxy docker container in your host machine. [link](https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion)
```bash
git clone https://github.com/evertramos/docker-compose-letsencrypt-nginx-proxy-companion.git
cd docker-compose-letsencrypt-nginx-proxy-companion
mv .env.sample .env
./start.sh
```

Clone your repository to host machine and build docker-compose.
```bash
git clone http://github.com/username/your_own_rails_repository
docker-compose build
docker-compose up -d
```

To see your live container log

```bash
docker ps
docker log -f processid
```

Scale your rails application to 5 replicas.
```bash
docker-compose up -d --scale app=5
```

Automated deploy task

After pushing repository to git and providing deployment information in `lib/tasks/deploy.rake` file.
You can automate above process.

```bash
rails deploy:production
```

## Testing

[rspec-rails](https://github.com/rspec/rspec-rails)
[factory-bot](https://github.com/thoughtbot/factory_bot/wiki)

> Run test specs

```bash
bundle exec rspec
```

---

[scale docker containers](https://pspdfkit.com/blog/2018/how-to-use-docker-compose-to-run-multiple-instances-of-a-service-in-development/)
