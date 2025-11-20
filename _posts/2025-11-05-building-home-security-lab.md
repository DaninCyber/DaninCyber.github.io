---
layout: post
title: "Building a Home Security Lab"
date: 2025-11-05
category: Network Security
tags: [lab, virtualbox, kali-linux, beginner]
author: Your Name
---

Setting up your own cybersecurity lab is essential for hands-on learning. Here's how to build one at home using free tools.

## What You'll Need

- A decent computer (8GB+ RAM recommended)
- VirtualBox or VMware
- Time and curiosity!

## Step 1: Install VirtualBox

Download from [virtualbox.org](https://www.virtualbox.org)

## Step 2: Get Kali Linux

Download the VirtualBox image from [kali.org](https://www.kali.org/get-kali/)

## Step 3: Vulnerable Machines

Download intentionally vulnerable VMs:
- Metasploitable 2
- DVWA (Damn Vulnerable Web App)
- VulnHub machines

## Network Configuration

Set up an isolated network:
1. Create NAT Network in VirtualBox
2. Put all VMs on same network
3. This isolates your lab from your home network

## Safety Tips

- Never attack systems you don't own
- Keep your lab isolated
- Don't use your main computer as the attacker

## What to Practice

- Port scanning with nmap
- Web exploitation
- Password cracking
- Network sniffing with Wireshark

Start with easier boxes and gradually increase difficulty. Happy hacking!