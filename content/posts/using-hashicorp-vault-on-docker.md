---
title: 'Using Hashicorp Vault on Docker'
date: 2021-06-30T20:00:00+00:00
draft: true
tags: ['Vault', 'Hashicorp', 'Docker', 'Linux', 'Containers', 'PKI', 'AD CS']
description: ""
cover:
  image: ""
  alt: ""
---

**In this post I will explain my Hashicorp Vault setup on Docker. It replaces my AD CS environment in my home lab.**

A few months ago I bought a new energy efficient Home Server based on an Intel Core i3-9100. It runs a hypervisor with Virtual Machines and some Docker containers.
As I want to containerize as much as possible and use HTTPS on my internal services, it was time to give Hashicorp Vault a spin!

The environment is based on two containers:

1. The vault container which is based on Hashicorp Vault
2. The vault-client container that I used to configure the vault.

The labels I used on the vault are optional if you are using Traefik (higly recommended!). Make sure to document the variables in your `.env` file.

```dockerfile
  vault:
    container_name: vault
    image: vault:latest
    depends_on: 
      - traefik
    volumes:
      - vault_data:/vault/file
      - vault_data:/vault/logs
    restart: on-failure:10
    environment:
      VAULT_ADDR: "http://0.0.0.0:8200"
      VAULT_API_ADDR: "http://0.0.0.0:8200"
      VAULT_LOCAL_CONFIG: >-
        {
            "ui": true,
            "backend": {
                "file": {
                    "path": "/vault/file"
                }
            },
            "default_lease_ttl": "168h",
            "listener": {
                "tcp": {
                    "address": "0.0.0.0:8200",
                    "tls_disable": "1"
                }
            },
            "max_lease_ttl": "720h"
        }
    cap_add:
      - IPC_LOCK
    healthcheck:
      retries: 5
    command: server # Run in PRD
    labels:
      - "traefik.enable=true"
      ## HTTP Routers
      - "traefik.http.routers.vault-rtr.entrypoints=https"
      - "traefik.http.routers.vault-rtr.rule=Host(`vault.$DOMAINNAME`)"
      - "traefik.http.routers.vault-rtr.priority=10"
      - "traefik.http.routers.vault-rtr.tls=true"
      ### Expose API without Azure AD Authentication
      - "traefik.http.routers.vault-api-rtr.entrypoints=https"
      - "traefik.http.routers.vault-api-rtr.rule=Host(`vault.$DOMAINNAME`) && PathPrefix(`/v1`)"
      - "traefik.http.routers.vault-api-rtr.priority=50"
      - "traefik.http.routers.vault-api-rtr.tls=true"
      ### Expose CRL & CA Endpoints without authentication
      - "traefik.http.routers.vault-ca-rtr.entrypoints=http"
      - "traefik.http.routers.vault-ca-rtr.rule=Host(`vault.$DOMAINNAME`) && PathPrefix(`/v1/pki`)"
      - "traefik.http.routers.vault-ca-rtr.priority=100"
      - "traefik.http.routers.vault-ca-rtr.tls=false"
      ## HTTP Services
      - "traefik.http.routers.vault-rtr.service=vault"
      - "traefik.http.routers.vault-ca-rtr.service=vault-ca"
      - "traefik.http.routers.vault-api-rtr.service=vault-api"

      - "traefik.http.services.vault.loadbalancer.server.port=8200"
      - "traefik.http.services.vault-ca.loadbalancer.server.port=8200"
      - "traefik.http.services.vault-api.loadbalancer.server.port=8200"

  # Use the vault client with 'docker-compose run --rm vault-client bash'
  vault-client:
    container_name: vault-client
    build: ./vault-client
    depends_on: 
      - vault
    volumes:
      - vault_cert_data:/data
    environment:
      VAULT_ADDR: "https://vault.$DOMAINNAME"
      VAULT_ADDR_HTTP: "http://vault.$DOMAINNAME"
      ROOT_CA_COMMON_NAME: $ROOT_CA_COMMON_NAME
      INT_CA_COMMON_NAME: $INT_CA_COMMON_NAME
      AZURE_AD_CLIENT_ID: $VAULT_AZURE_AD_CLIENT_ID
      AZURE_AD_DISCOVERY_URL: $AZURE_ISSUER_URL
      AZURE_AD_DEFAULT_ROLE: $VAULT_AZURE_AD_DEFAULT_ROLE
      AZURE_AD_CLIENT_SECRET: $VAULT_AZURE_AD_CLIENT_SECRET
      VAULT_AZURE_AD_ROLE_NAME: $VAULT_AZURE_AD_ROLE_NAME
      DOMAINNAME: $DOMAINNAME
      ORGANIZATION: $ORGANIZATION
      BASE_DOMAIN_NAME: $BASE_DOMAIN_NAME


volumes:
  vault_data:
  vault_cert_data:
```

The dockerfile for the vault-client is very simple:

```dockerfile
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y software-properties-common curl gnupg2 jq nano keychain && \
  curl -fsSL https://apt.releases.hashicorp.com/gpg | apt-key add - && \
  apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main" && \
  apt-get update && apt-get install -y \
  vault && \
  setcap cap_ipc_lock= /usr/bin/vault

COPY run.sh ./
COPY admin-policy.hcl ./
```
