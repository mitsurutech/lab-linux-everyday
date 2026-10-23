# Everyday Linux commands lab: ls, grep, tail -f, ssh, scp and kill in one Ubuntu VM

[English](README.md) | [Français](README.fr.md) | [日本語](README.ja.md) | [Español](README.es.md)

[![check](https://github.com/mitsurutech/lab-linux-everyday/actions/workflows/check.yml/badge.svg)](https://github.com/mitsurutech/lab-linux-everyday/actions/workflows/check.yml)

A ready-made **Linux commands lab** for classrooms, from the [MitsuruTech Learning Platform](https://mitsurutech.co.uk/learning), where schools and colleges give every student their own Ubuntu machine and a terminal in the browser. It has something real for every command a working software engineer types without looking it up: **walk and search files** (`ls`, `cd`, `find`, `grep`), **read a log that is still being written** (`tail -f`), **find and stop a process** (`ps | grep`, `kill`, `kill -9`), **fetch and unpack files** (`curl`, `wget`, `zip`, `gzip`), and **log in to another account and copy files to it** (`ssh`, `scp`). Nothing is installed on the student's computer.

## What is on the machine

| What | Where | Used for |
| --- | --- | --- |
| A log with an hour of lines that grows every two seconds | `/var/log/test.log` | `tail`, `grep`, counting errors |
| An archive and a file to compress | `~/test.zip`, `~/test` | `unzip`, `gzip` |
| A small tree to walk about in, and a folder that is safe to delete from | `~/projects`, `~/scratch` | `ls`, `cd`, `find`, `cp`, `mv`, `rm -rf` |
| A web server on port 8000 holding two small files | `localhost:8000` | `curl`, `wget` |
| Two processes, one of which ignores a plain `kill` | `lab-worker`, `lab-stubborn` | `ps`, `kill`, `kill -9` |
| A second account, `dev`, reached by key as `devbox` | `ssh devbox` | `ssh`, `scp` |

The second account is on the **same machine**, not a second one: the commands are the same and a second VM would only add waiting. The lab has no check and no task. The five lessons on the platform are the activity, and a teacher who wants a mark sets a hand-in of their own.

## What is in the file

`linux-everyday.lab.yaml` is a whole **VM lab definition**, exactly what the platform runs:

| Key | What it is |
| --- | --- |
| `cpus`, `memory`, `disk` | the size of each student's VM: 1 CPU, 1024 MB and 10 GB |
| `open` | the ports that open in the browser: none, the lab is the terminal |
| `setup` | a script run once, as root, the first time each student's VM starts: it installs a few packages from Ubuntu's archive, makes the log, the files, the two processes, the web server and the second account, and writes a README in the home folder |

## Using it on the platform

1. In your module, add a task and choose the **Ubuntu VM lab** card.
2. Press the sample, or paste the contents of `linux-everyday.lab.yaml`. Using a sample replaces the text, and Undo brings yours back.
3. Publish and try your own copy first. Every student gets a VM of their own, kept between sessions.
4. Assign it like any task, or open the lessons in the library and press Run beside a command.

The help manual's [page for this lab](https://mitsurutech.co.uk/help/lab-linux-everyday), its [guide to Ubuntu VM labs](https://mitsurutech.co.uk/help/labs) and its [sample labs page](https://mitsurutech.co.uk/help/sample-labs) cover the rest. No college account yet? [Your first year is free](https://mitsurutech.co.uk/pricing) for up to 50 students, and [signing up](https://mitsurutech.co.uk/signup) takes an email address.

## Checking the file

On every push, `.github/workflows/check.yml` checks that the file is valid YAML with the keys above and that `setup` is inside the platform's 16 KB limit. It does not boot a VM: that is done on the platform's own machines.

## What does not work in a lab

The VM reaches Ubuntu's package archive, PyPI, npm and GitHub, and nothing else, so a lab cannot be pointed at a host on the internet. That is why the web server is inside the lab.

## About

Made by [Mitsuru Technologies](https://mitsurutech.co.uk) for the [MitsuruTech Learning Platform](https://mitsurutech.co.uk/learning): Python, Java, Go, Node, SQL and Linux in the browser for schools and colleges, with container labs, VM labs, web apps deployed from GitHub, and quizzes that mark themselves. Try code with no account in the [playground](https://mitsurutech.co.uk/playground).

More labs from the same place: [lab-linux-admin](https://github.com/mitsurutech/lab-linux-admin), [lab-linux-privesc](https://github.com/mitsurutech/lab-linux-privesc), [lab-incident-response](https://github.com/mitsurutech/lab-incident-response), [lab-netlab](https://github.com/mitsurutech/lab-netlab), [lab-git-gitea](https://github.com/mitsurutech/lab-git-gitea) and [lab-sample](https://github.com/mitsurutech/lab-sample).

## Licence

This work is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/). You may share it and adapt it for learning and teaching, if you credit Mitsuru Technologies Ltd, do not use it commercially, and share anything you make from it under the same licence. The full text is in the `LICENSE` file.

`zip`, `unzip`, `curl`, `wget`, `openssh-server`, `vim` and `python3` are installed from Ubuntu's archive when a VM starts; nothing of them is distributed here.
