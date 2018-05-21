---
layout: post
title: "How to Add Subdomains To Your Linode Hosted Nginx Server"
date: 2015-01-28 16:14:01
categories: General
meta: "How to Add Subdomains To Your Linode Hosted Nginx Server"
---

<em>This tutorial assumes you have already <a href="https://www.linode.com/docs/getting-started">set up your own Linode</a> and <a href="https://www.linode.com/docs/websites/nginx/nginx-and-phpfastcgi-on-ubuntu-12-04-lts-precise-pangolin">configured Nginx</a> on it already. If you haven't, don't worry there are more great walkthroughts on the subject online. For the purposes of this tutorial I will refer to 'www.koendecouck.com' as the top-level host and 'example.koendecouck.com' as the subdomain we try to set up.</em>

It's relatively to create subdomains once you have a website already up and running. None the less I decided to write a mini-tutorial on it because the steps might not always be immediately intuitive. You should have a webserver (<a href="http://nginx.org/">Nginx</a>), a webhost (<a href="http://www.linode.com">Linode</a>) and DNS provider (<a href="http://www.namecheap.com">Namecheap</a>) already. But where do you start?

<strong>Create a new Linode A record for your subdomain.</strong>
<em>Contrary to what you may think, you don't actually need to consult your DNS provider (e.g., Namecheap) for this. It took me hours before I figured out subdomains are actually handled by the webhost (e.g., Linode) and didn't require any top-level tampering. It doesn't help that Namecheap also offers their own hosting services so it's easy to get misdirected by their own online tutorials. Ignore those, instead one part takes place through Linode's web interface, the second part requires some tweaking to Nginx's configuration files.</em>

To start navigate to your <a href="https://manager.linode.com/">Linode manager</a>. Select the 'DNS Manager' tab and click on your top-level domain (www.koendecouck.com). Scroll down to 'A/AAAA Records'. Find the line stating 'www' and copy the corresponding IP address. In the right-bottom corner click 'Add a New A Record'. A new page opens up.

Under 'host' type in the subdomain you want. For example if you'd like the domain 'example.koendecouck.com', type 'example' as the host. For 'IP Address' paste the top-level domain's ip address you copied earlier (e.g., 104.237.137.73). Save changes.
That's it for Linode's side of the deal. It will take about 15 minutes for the subdomain to become active. We'll set up your Nginx configuration.

<strong>Create a new Nginx server block</strong>
'Server blocks' are a Nginx term for what Apache users call 'Virtual hosts'. It's common to see the terms intermixed in tutorials. Regardless of the name, it requires firing up your terminal at this point. Connect to your webserver.
<font color=”#008080″><code>ssh koen@www.koendecouck.com</code></font>

Navigate to your server's 'sites available' folder.
<font color=”#008080″><code>cd etc/nginx/sites-available</code></font>

This folder contains all your domain's server blocks. You should have one already with the name of your existing site. If not, then you should at least have a default file there.
<font color=”#008080″><code>dir</code></font>

Copy the existing server block and open it up with an editor.
<font color=”#008080″><code>sudo cp www.koendecouck.com example && sudo vim example</code></font>

Change the server_name, access_log, error_log and root to reflect the updated path. (Press 'i' to activate vim's insert mode). Don't touch anything else.
<font color=”#008080″><code>server {
server_name www.example.koendecouck.com example.koendecouck.com
access_log /nginx/www/example/logs/access.log;
error_log /nginx/www/example/logs/error.log;
root /nginx/www/example/public;
</code></font>

Press 'Esc' to get out of insert mode, then type ':wq' to save your changes and quit the vim editor.

Next, create a symbolic link between your subdomain's sites-available and its sites-enabled file.
<font color=”#008080″><code>sudo ln -s sites-available/example.conf sites-available/example.conf</code></font>

Get out of your Nginx's configuration directory and navigate to where the web files are stored. This path may vary a bit depending on where you chose to install.
<font color=”#008080″><code>cd nginx/www</code></font>

Let's get our subdomain project started. Create a new directory and do basic setup: setting the owner and permissions. 
<font color=”#008080″><code>sudo mkdir example && sudo chown koen:koen example && sudo chmod 775 example</code></font>

Let's dive in.
<font color=”#008080″><code>cd example</code></font>

Create an index file for preview purposes.
<font color=”#008080″><code>vim index.html</code></font>

Tap 'i' for vim's insert mode, then type 'hello world'. Tap 'esc'+':wq' to write and quit.

<em>Optional: Personally I like to keep the configuration file contained in the same project folder as well. You can't really move the configuration file from its etc path, but you CAN create another symbolic link to it. This makes it easier to edit later.</em>
<font color=”#008080″><code>mkdir app && sudo ln -s sites-available/example.conf nginx/www/example/app/</code></font>

Restart Nginx
<font color=”#008080″><code>sudo service nginx restart</code></font>

You may have to wait a few more minutes while your Linode setup becomes active. Then try accessing your new subdomain in a browser: example.koendecouck.com
If all went you should see 'hello world' popping up. Congratulations, your subdomain is active and ready to be used!
