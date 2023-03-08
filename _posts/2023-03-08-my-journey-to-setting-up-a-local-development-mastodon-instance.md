---
title: "My Journey to Setting up a Local Development Mastodon Instance"
layout: post
author: chrispelatari
categories: [mastodon, development, ruby, rails, postgresql, nginx, letsencrypt, vagrant]
---

![Mastodon Development Instance](/assets/images/mastodon_development.png)

I've been looking for a way to update my skills in web development recently while searching for a new job. I've been working in the IT industry for over 20 years now, mostly in the .NET sphere. I noticed that I was turning down a few really interesting opportunities because of my lack of accomplishments with specific modern front end frameworks, including React.js and Angular. I have a few projects that I've worked on in the past that I could use to demonstrate my skills, but I wanted to do something more. 

I wanted to build something from scratch, and I wanted to do it in a way that I could share with others. I also wanted to do it in a way that I could use to demonstrate my skills to potential employers. 

So I decided to build a local development instance of [Mastodon](https://joinmastodon.org/); a free, open-source social network. I've been using Mastodon for a few months now, and I really like it. It currently feels like 2008-2010 Twitter, when it was still fun and interesting. 
> And not run by Elon Musk.

It was not an easy task, but I learned a lot along the way. I'm going to share my journey with you, and hopefully you'll find it useful.

## Base Environment : OS X

I decided to use my MacBook instead of my Windows box or the Ubuntu Linux that I installed on a Mac Mini. I might change my mind later. I'm not sure yet. This was more of a proof of concept: can I even get all of the moving parts to work together? I'm not sure if I'll actually use this instance for anything other than testing and development.

## Guest Environment : VirtualBox

I'm using VirtualBox as the virtualization provider for Vagrant with the Ubuntu 18.04 LTS box, which is a 64-bit version of Bionic Beaver.

## Host Environment : Vagrant

I wanted to build this on my Mac, but I also wanted to be able to easily destroy and rebuild the environment if I needed to. So I decided to use [Vagrant](https://www.vagrantup.com/).

Vagrant is a tool for building and managing virtual machine environments in a single workflow. It allows you to define a virtual machine configuration in a single file, and then spin up the virtual machine with a single command.

I used homebrew to install it:
```bash
    brew cask install vagrant
```

I then created a new directory for my project, and created a new Vagrantfile in it:
```bash
    mkdir vagrant
    cd vagrant
    vagrant init
```

I then edited the Vagrantfile to use the Ubuntu 18.04 LTS box:
```ruby
    Vagrant.configure("2") do |config|
        config.vm.box = "ubuntu/bionic64"
    end
```

I customized the Vagrantfile a little more using the [Vagrantfile for Mastodon](https://github.com/mastodon/mastodon/blob/main/Vagrantfile) as a reference.

I started the virtual machine:
```bash
    vagrant up
```

I then SSH'd into it:
```bash
    vagrant ssh
```

## Installing Mastodon from Source

I decided to install Mastodon from source, instead of using the Docker image. I wanted to learn more about the underlying technologies, and I wanted to be able to customize the installation. Also, I wanted to be able to use the latest version of Mastodon, instead of the version that was available in the Docker image. To accomplish this, I needed to install Ruby, Rails, and PostgreSQL.

I started with the [Mastodon Installation Guide](https://docs.joinmastodon.org/admin/install/). It took me a few tries to get it right, but I was able to get it working in the end.

Probably the most difficult challenge was getting certbot to issue a certificate for my domain. I was able to get it working, but I had to use the `--manual` option, and I had to manually create the DNS records for the challenge. I'm not sure if there is a better way to do this, but it worked for me. I found a pretty decent guide at [esc.sh](https://esc.sh/blog/letsencrypt-ssl-for-local-domains/) that got me most of the way there. (see above)

## webpacker woes

Well now I have a working Mastodon instance, but webpacker is refusing to spin up, claiming that a service is already running on the port provided in the config file. This is my first time even looking at webpacker, having most of my experience in ASP.NET MVC. So I looked at the config/webpacker.yml file, and I noticed that the port was set to 3035. I looked at the nginx config file, and I noticed that the port was set to 3000. These aren't the same ports, what gives? This is usually the part of a blog post where I would say something like "I spent hours trying to figure this out, but I finally figured it out." And I did. But I'm not going to bore you with how. This is already one of the longest blog posts I've ever written. 

I tried several different approaches and ended up having to restart the webpacker service a few times. Eventually it started working. I didn't take note of what was the winning magic incantation, but after a couple of restarts I have a working mastodon instance.

![It lives!](/assets/images/mastodon_development_it_lives.png)

## Conclusion

I don't fully understand how all of the pieces fit together yet, but I'm getting there. I'm going to continue to work on this project, and I'll update if I come across anything interesting. 

It felt good to hack on something that gave me that feeling of accomplishment that I used to get when I was a [young developer](https://chris.pelatari.com/2003/02/11/Nearing-completion.html). If you've read this far, you're a champ. Thanks fam.