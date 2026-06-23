# Secure Mission Data Platform on AWS

## Project Purpose

This repository documents my long-term AWS solutions architecture case study for a simulated secure mission data platform.

The project is being built from the ground up, starting with Linux and local server fundamentals before progressing into AWS networking, databases, security, cost modeling, Terraform, validation testing, and architecture documentation.

The goal is to develop and document a realistic architecture workflow: understanding requirements, comparing design options, explaining tradeoffs, validating decisions in a lab environment, and presenting the final recommendation clearly.

## Simulated Customer Scenario

The simulated customer is a small defense-adjacent logistics organization that needs a secure platform to store and manage mission asset data.

The customer needs a solution that supports:

* Controlled access to sensitive data
* Private and secure data storage
* Backup and recovery planning
* Basic monitoring and logging
* Cost-aware architecture decisions
* A realistic MVP design with a clear production upgrade path

## Architecture Focus Areas

This project connects technical fundamentals with architecture-level decision-making.

Key focus areas include:

* Linux server fundamentals
* Secure server access
* Networking and traffic flow
* AWS VPC design
* EC2, S3, RDS, IAM, CloudWatch, and CloudTrail
* Cost modeling with AWS Pricing Calculator
* RDS backup and restore planning
* Terraform-based infrastructure rebuild
* Security review and risk analysis
* Architecture validation in a sandbox environment
* Technical and business-facing presentation

## Learning Model

Every concept in this project follows the same process:

1. Learn the concept
2. Apply it to the flagship project
3. Reuse earlier fundamentals
4. Test or validate the behavior
5. Document the result
6. Commit the work to GitHub

This structure is meant to keep Linux, networking, databases, security, cost modeling, Terraform, and AWS connected through one architecture case study instead of treating each topic as a separate isolated skill.

## Current Phase

Current phase: Linux foundation and local lab setup.

I am currently working on VirtualBox, terminal basics, Linux command structure, man pages, snapshots, safe rollback habits, and early documentation standards.

These fundamentals will later map into AWS concepts such as EC2, security groups, VPC traffic flow, CloudWatch logging, RDS recovery, Terraform rebuilds, and sandbox validation.

