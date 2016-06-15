# Clarifai payable micro service example

This is a working prototype that shows how to wrap an existing API and sell those services for micro payments.

Requirements:
- API Keys from Clarifai.com, they have free tier accounts.
- Web Server with:
  - git
  - docker and docker-compose
  - 21.co software, and initialized wallet

Checkout the docker compose file to see how it works.

## Setup

Install 21.co and setup wallet
```
curl https://21.co | sh
21 login
```

Install docker and docker-compose:  https://docs.docker.com/compose/install/

Clone this repo, configure and run it.
```
git clone https://github.com/pennyfx/clarifai-reseller.git
cd clarifai-reseller
# MODIFY docker-compose.yaml file, adding your keys and hostname(if applicable)
vi docker-compose.yaml
docker-compose up -d
```

## Buy an API call from yourself
```
21 buy http://0.0.0.0:8928/payable/tag?url=http://i.imgur.com/aNJjbfC.jpg
```

You can run this from your home computer if you like.  I used AWS since they have a free tier.

## Easy config

config.yaml allows you to easily add more services, rename routes or change fees.  One could potentially have many different services behind this one proxy.

## Why

The main goal of this project was to show that it's possible to wrap REST APIs pretty easily, once you have a payable proxy.  The Clarifai wrapper only handles auth and basic request normalization.

The main drawback to this solution, is the number of http requests required to complete it.   Obviously, integrating `payment required` directly into our apps is a more efficient method, but 21.co is only written in Python at this stage, so it's limited.

Another interesting aspect of this experiment, is packaging micro-services as complete docker installs and sharing them. If we had 100 people running this same service setup, we can begin to build other services that parallelize requests to nodes of this type, but only if they are identical. Docker-compose.yaml is an easy way to ensure all services are the same.

Imagine a future, where you can pick and choose various payable services to run on your computer and earn bitcoin for it.   It's pretty incredible what we can do with the payable web.

## License

MIT

