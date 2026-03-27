# Vaultwarden Server

Self-hosted password manager project using Vaultwarden.

## Purpose

This project is part of my self-learning portfolio in:

- Linux
- homelab infrastructure
- Docker
- reverse proxies
- cloud deployment
- web services

## Stack

- Vaultwarden
- Docker Compose
- Nginx
- Azure VM
- Cloudflare DNS
- Let's Encrypt

## Deployment Summary

This Vaultwarden instance is deployed on an Azure VM and served securely through Nginx with HTTPS.

## Access

- https://vault.greycell.online

## What I Learned

- How to deploy a containerized service with Docker Compose
- How to keep a service private on localhost and expose it through Nginx
- How to connect DNS records through Cloudflare
- How to issue and troubleshoot TLS certificates with Certbot
- How to back up persistent Docker data
- How to document and track infrastructure projects with Git and GitHub

## Notes

- Vaultwarden runs on `127.0.0.1:8082`
- Nginx reverse proxies traffic from `vault.greycell.online`
- HTTPS is enabled with Let's Encrypt
- Secrets and live data should stay out of GitHub
