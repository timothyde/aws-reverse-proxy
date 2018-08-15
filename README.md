# Reverse Proxy Configuration with Traefik

This is a step by step guide on how to run a reverse proxy with Traefik

## Getting Started

These instructions are meant to be used on an AWS Linux EC2 Instance. The necessary commands may vary depending on your use case.

### Prerequisites

First and foremost, you need a server which you can SSH into.
Since we are using the Traefik Docker Container, we need to install Docker first.
Use [this guide](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/docker-basics.html#install_docker) if you need assistance.

Next up, we need docker-compose.
Use [this gist](https://gist.github.com/benfogel/041e3c4b8b856cdcdfd8d9d5aa0a7f73) if you need assistance.

To create a password for the Traefik admin tools, we are gonna use **htpasswd**, which can be installed via

```
sudo yum install httpd-tools
```

### Installing

First up, create a password for your admin user with the following command, replacing <your_secure_password> with your password and save the output for later.

```
htpasswd -nb admin <your_secure_password>

Output
admin:$apr1$ruca84Hq$mbjdMZBAG.KWn7vfN/SNK/
```

Use the above output and replace <your_encrypted_password> with the newly encrypted password in the line

```
  users = ["admin:<your_encrypted_password>"]
```

inside of traefik.toml.
Also inside of traefik.toml, replace the email with yours:

```
  email = "<your_email>"
```

Inside of docker-compose.yaml, replace the traefik.frontend.rule label with your domain

```
    labels:
      ...
      - "traefik.frontend.rule=Host:monitor.<your_domain>"
      ...
```

## Deployment

-

## Built With

- [traefik](https://traefik.io) - used as a reverse proxy

## Authors

- **Timothy Krechel** - _Initial work_ - [timothyde](https://timothy.de)

## License

This project is licensed under the MIT License.

## Acknowledgments

- Hat tip to anyone whose code was used
- Inspiration
- etc
