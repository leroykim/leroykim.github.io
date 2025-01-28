---
layout: post
title: Shell script to attach AWS EBS volume to EC2 instance 
categories: [Large Language Models (LLMs), AWS]
tags: [AWS, EC2, EBS]
author: Dae-young Kim
comment: true
---

```bash
#!/bin/bash
# Run `chmod +x mount_ebs.sh` to make it executable.

MOUNT_DIRECTORY="EBS"
EBS_PATH="/dev/nvme1n1"

echo "########################################"
echo "# Attaching Elastic Block Store (EBS). #"
echo "########################################"
echo "Mount directory: $MOUNT_DIRECTORY"
echo "EBS path: $EBS_PATH"
echo ""

echo "% lsblk"
lsblk
echo ""

echo "%sudo mount --source $EBS_PATH --target $MOUNT_DIRECTORY"
sudo mount --source $EBS_PATH --target $MOUNT_DIRECTORY
echo ""

echo "% ls $MOUNT_DIRECTORY"
ls $MOUNT_DIRECTORY
```