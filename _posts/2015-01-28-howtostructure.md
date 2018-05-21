---
layout: post
title: "How To Structure App Files"
date: 2015-01-28 17:03:00
categories: General
meta: "how to structure app files"
---

<em>Note: I've tweaked this particular structure from the <a href="https://levels.io/how-i-build-my-minimum-viable-products/">file structure proposed by Pieter Levels</a>, who himself adapted it from other sources.</em>

I'm super-organized and a perfectionist in nature. I like logical structures, I see beauty in it. Most projects require more or less the same resources and so it made sense to develop a common file structure for them. For now this is the one I use, but this is subject to change:

<strong>/app/</strong>
This includes all front-end (SCSS, JS), back-end code (PHP, Node.JS) + the Nginx configuration file project.conf uses. Nginx’s config file acts as a natural router to route specific subdomain URLs to certain PHP files. This works in tandem with A-records configured through Linode's web interface.

Like Pieter, I use CodeKit to monitor this folder and automatically pre-process/minify/compile the SCSS and JS files to the /public/assets/ folder

<strong>/config/</strong>
Configuration files

<strong>/data/</strong>
This includes all datasets used in the project. These are JSON text files for quick-and-dirty projects (which most are). The string in the JSON filename is an <a href="http://en.wikipedia.org/wiki/MD5#MD5_hashes">MD5 hash</a> of what it’s about. I may set up a SQLite (one file) or full-blown mySQL database as needed. I think the main difference lies in performance and data security? JSON files are faster to write up and edit however, which is an advantage when you iterate fast.

<strong>/lib/</strong>
This includes all back-end server-side libraries and stuff I didn’t make myself and don’t want to edit. Examples: Stripe’s library for payment processing and Twitter’s OAuth library. Libraries are included from this folder by apps in the /app/ folder.

<strong>/logs/</strong>
Scheduled server-side cron jobs write their output to txt files in this folder. 
An example cronjob looks like this:
<font color=”#008080″><code>
php -f /srv/http/domain.com/workers/doStuff.php> /srv/http/domain.com/logs/doStuff.txt
</code></font>

As you can see the cronjob shell scripts hold commands for the workers, which reside as php files in their own folder.

<strong>/press/</strong>
Screenshots of project press mentions.

<strong>/process/</strong>
This folder documents my design-and-development process. It contains all the rough pre-development assets like mock ups in Photoshop and Sketch of the interface and logo designs.

<strong>/public/</strong>
All public files that are viewable by users.
<strong>/public/assets/</strong>
This includes all public asset files. That means pretty much everything used by the front-end. CSS for styling, JS for client-side scripting, images in PNG, cgi-bin folder for Python files etc. This should all be publicly accessible. All JS/CSS files are pre-processed from the /app/ folder.

<strong>/ssl/</strong>
Holds the https ssl certificate.

<strong>/workers/</strong>
This includes all php workers that do run in the background by scheduled cron jobs. Examples: sending out email queues, downloading data on a daily basis (scraping), uploading data (backups).