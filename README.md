# VPC-Traffic-flow-and-security

Welcome to your very first AWS networking project!

You'll dive into the core of AWS networking by creating your very own Virtual Private Cloud (VPC).

Setting up and managing a VPC is a vital skill for anyone looking to master cloud infrastructure. Today, you'll learn how to set up and configure a VPC from scratch.

## Introduction

#### What is Amazon VPC and how is it useful?

Amazon Virtual Private Cloud (Amazon VPC) allows you to create isolated virtual networks within the AWS cloud infrastructure. It provides you with control over your virtual networking environment, including selection of IP address ranges, configuration of route tables, and management of network gateways. Amazon VPC is fundamental for securely hosting your AWS resources and connecting them to your on-premises infrastructure or other cloud environments.

Lets get ready:

1 - ☁️ Create an Amazon VPC.\
2 - 🥅 Create a public subnet.\
3 - 🚪 Create an internet gateway.\
4 - 🚏 Create a route table.\
5 - 👮‍♀️ Create a security group.\
6 - 📋 Create a Network ACL (Network Access Control List).

  <img width="725" alt="Screenshot 2024-07-04 at 10 37 30 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/0710c780-d72c-401f-9308-b763f5904a02">

## Step: 1 My first VPC

VPCs are virtual private cloud that are located in isolated areas of AWS cloud to keep my AWS resources safe and secure.

There was already a default VPC in my account ever since my AWS account was created. This is because AWS has setup default VPC to allow me to deploy resources like EC2 instances/RDS databases right away without having to create my own VPC.

To set up my VPC, I had to define an IPv4 CIDR, which means a range of IP addresses that my VPC can allocate to the resources deploy into my VPC.

<img width="1179" alt="Screenshot 2024-07-04 at 8 00 23 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/6092c6c1-0eab-4e61-8165-f8d3dc8b2c2e">

## Step: 2 Subnets

Subnets are subsections of my VPC, just like how neighbourhood are subsections of a city.

There are already subnets existing in my account, one for every Availability zone in the Region that I’ve setup in my VPC in. Since my region is Oregon (US-west-2), which has 4 Availability Zones, I have four default subnets already

I named my subnet myPublic Sub, but that doesn’t automatically make my subnet a public subnet. For a subnet to be considered public, it has to connect to an internal gateway.

<img width="1394" alt="Screenshot 2024-07-04 at 8 06 38 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/4b947895-f079-4e4c-8bb4-5b27a4ae7f83">

## Step: 3 Internet Gateway

Internet gateway are the key VPC components that allows internet access for the resources in my VPC/subnet. An internet gateway is also how users in the public can access my resources in a public subnet.

Attaching an internet gateway to a VPC means it can now access the internet. The EC2 instances with public IP addresses also become accessible to users, so your applications hosted those servers become public too.

While I’ve set up an internet gateway and attached it to a VPC, I still have to set up route tables. Route tables will help EC2 instances or other resources in my VPC to find their way to the internet gateway that is attached to my VPC.

<img width="955" alt="Screenshot 2024-07-04 at 6 02 16 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/5f85ddc5-0575-4c84-a6e4-95f451ddf778">

## Step: 4 Routing table

Route tables are like GPS that directs traffic within my VPC to the correct destination. 

Routes tables are needed to make a subnet public because subnet needs to make a route to an internet gateway to make a route public. A route table is the only way to established connection.

A route table is made up of routes, which are defined by its destination and target:
* The destination is the range of IP addresses that traffic in my VPC is trying to connect.
* The target is a road or path that the traffic will have to take to get to its destination.

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 and a target of my VanshP IG (internet gateway)

<img width="879" alt="Screenshot 2024-07-04 at 6 28 26 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/699ce1af-a09e-4b31-8871-5df899f300fd">

<img width="868" alt="Screenshot 2024-07-04 at 6 29 34 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/3ed3aed7-54e8-4ff8-9f6f-a8b022508896">


## Step: 5 Security Groups

Security groups are like security guards that monitor both inbound and outbound traffic at the resource level ie. every single resource in a subnet/VPC has a security group.

Security groups control traffic flow using two types of rules:
* Inbound rules are the rules that restrict inbound traffic eg. user visiting a web app I’m hosting.
* Outbound rules are the rules that monitor/restrict outbound traffic eg. my web app requesting data from a public source.

By default, an outbound rule will allow all outbound traffic.

I also configured an inbound rule that allows all inbound HTTP traffic.

<img width="854" alt="Screenshot 2024-07-04 at 7 05 36 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/c3d41c5d-782b-488e-b69e-9ac4aa9a917e">
<img width="1314" alt="Screenshot 2024-07-04 at 7 11 58 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/bca1a429-4426-4a89-95d3-1a7fe2292dfd">

## Step: 6 Network ACLs

Network ACLs are like community policemen that secures my network at a subnet level.

The difference between a security group and a network ACL is their scope i.e a security groups secures my network at resource level, while network ACLS secures my network at the subnet level.

Having both network ACLs and security groups is a good security best practice because it creates a dual layer of security that makes sure inbound/outbound traffic go through at least two checks.

Similar to security groups, network ACLs use inbound and outbound rules:
* A default network ACL’s inbound rule is set up to allow all incoming traffic.
* A default network ACL’s outbound rule is set up to allow all outgoing traffic.
* In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all incoming/outgoing traffic.

My network ACL’s inbound rule
<img width="864" alt="Screenshot 2024-07-04 at 7 38 42 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/b47ca89b-f204-4ba9-8753-50ab227e17dd">

My network ACL’s outbound rule
<img width="866" alt="Screenshot 2024-07-04 at 7 39 37 PM" src="https://github.com/vanshp968/VPC-Traffic-flow-and-security/assets/147680002/77f19ee7-3cd5-4be7-92cc-655d281c6ed5">


## Key Learnings

* I Learn how to set up a virtual network environment in AWS, defining IP address ranges and configuring subnets to segregate resources effectively.
* I understand the process of creating an internet gateway and associating it with your VPC to enable communication with external networks securely.
* I gain insights into configuring route tables to direct traffic within the VPC and between the VPC and external networks, ensuring efficient data flow.
* I explore the use of security groups to control inbound and outbound traffic at the instance level, enhancing network security by defining access rules.
* I learn to set up and manage Network ACLs, which act as a firewall for controlling traffic at the subnet level, providing an additional layer of security and control.

These learnings equip you with fundamental skills in AWS networking, essential for building secure and scalable cloud infrastructures.
