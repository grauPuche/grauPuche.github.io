# flyBy

# What is this for

Learning _web development_ in this day and age is something that lots of people are already doing, but we only know half of it. We only dive into the client-side end of the deal, so we know how to use HTML and javascript, but server-side is never mentioned.

So this is what this is for, what is a server, what it does and why should you even think about them.

# Let the nerds take care of that.

To that I would say no, a server is basicly a computer somewhere that stores information that when requested, gets 'served' to the client. That is basicly how the internet works, A bunch of computers in places giving you stuff when you ask for it. 

A fearly easy action that besides its value most people that work in projects that require a service like this don't really know the basics of it.

So here we are, trying to tell you what this is and how to set up an eviroment for you to play around with all this. 

# Digital Ocean

Either you left cause you don't care about this or you wanna work in this soon to be nightmare.

So lets dive into [digitalOcean](https://www.digitalocean.com) (get it?).

## droplets.

A droplet is virtual computer. An emualtion of an actual computer set up inside a real much more powerfull machine. this allows getting your hands into a computer very fast and easily. In this case one with a public IP and and a easy access from anywhere. This allows to create servers and to put them up in no time.

That is what we are going to use to create the server and play around with [node.js](https://nodejs.org/en/) and NginX.

Getting a droplet up and running is pretty quick, just go to [digitalOcean](https://www.digitalocean.com) sing up.

Having a droplet costs money but luckily if you have a **.edu ** email linked to your github account you can get a **$50 credit** thanks to the [GitHub Education Pack](https://education.github.com/pack) . If you don't have a .edu email can get **$10** [here](https://m.do.co/c/50edef5599af) .

 _all this only works if you have never used digitalOcean._ 

Go get your free money (I'll be here waiting)

![](https://static.notion-static.com/ae310de0d1b34e259cc523b7eff59507/Screen_Shot_2017-10-21_at_19.47.00.png)

Once you have your code, just go to the billing section on settings and look for the window where to add the code. You should be notified once added. 

![](https://static.notion-static.com/30429d230db246e0833e43eac392ec61/Screen_Shot_2017-10-21_at_19.55.24.png)

---

So... You have money to get a droplet up and running now. Creating a droplet is fairly simple, you go to the create tab, select droplets, and then you set it up.

We are going to be using the basic **Ubuntu** **16.04.3 x64 ** system and the **$5 per month** option. You can upgrade later on if you wish to do so. The rest of info is not relevant right now, so you can leave the default settings.

![](https://static.notion-static.com/7758ca3b5ab3413fa4d2c7b526f202a9/Screen_Shot_2017-10-21_at_19.36.33.png)

![](https://static.notion-static.com/11744a7e0f914b3a9a66518ed8229536/Screen_Shot_2017-10-21_at_19.36.47.png)

Congratulations you have your first VPS up and running.

# SSH

Secure Shell is what we are going to be using to acces our server, this allows us to access a computer on a secure way through a unsecure network.

ssh is done through the command line; and to do that you need your server IP and the user name. If you have followed everything properly if you go to your email you should have recieved and email form digitalOcean giving you your access info.

![](https://static.notion-static.com/06e9616fee3f45d0b6266e40116d777f/Screen_Shot_2017-10-21_at_20.20.20_copy.png)

It should look like this

Now that you have that information open terminal and do the following:

    ssh root@111.222.333.444

after that you are gonna be asked for your password and then you will be asked to change it again. because you know. sending paswords via email is not the best of ideas.

# new user

 **root ** is the the main user in a OS, so it is not a very good idea to be playing around with it, specially if you happen to be a novice like we are.

This means that the standard procedure is to create a new user every time you start a new system.

    adduser _username_

Not all users are born equal so new ones do not have the same privileges as the root user. This means that in order to proceed we need to give **sudo** privileges to the new user so we can use it almost as the same way as the root user.

    usermod -aG sudo _username_

now the new user has a better chance at changing the system, it is more powerful, as long as you use "sudo" before those commands that require the privileges.

 _If you want to make your system a bit more secure you should generate a ssh-key. check _ [_this tutorial_](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04) _ for that_ .

now that you have the new user up and running, logout and ssh again with the new user.

    ssh _newuser_@111.222.333.444

# Node js

Node is a javasacript **open source server framework** that runs on the [V8](https://developers.google.com/v8/intro) engine, this allows to use javascript to create contents outside the browser.

It is mainly used for server-side programs and it has one of the biggest open source package libraries there are; [npm](https://www.npmjs.com) .

To **install node** we need the script to do so, this script is on a website that means we need to use **curl. ** make sure that yo are in your home directory. 

 **_curl_** _ is a tool to transfer data from or to a server that uses the most used protocols in webservers._ 

    curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh

Once we get this script we run it. This will prep the system so we can install **node** normally with **apt-get.** 

 **_apt-get_** _ is the package manager for linux._ 

    sudo bash nodesource_setup.sh

    sudo apt-get install nodejs

Now that node is installed we can proceed to build the first server but to make sure everything you download with npm works, is better to also get the **build essential** package.

    sudo apt-get install build-essential

# 1stServer.js

Everything is on place to start creating the server, first we need a place where to keep the server file, therefore we need a directory, to do that we use the command **mkdir** (make directory)/

    mkdir 1stServer

    touch 1stServer.js

    nano 1stServer.js

    var http = require('http');
    
    http.createServer(function(request, response){
     response.writeHead(200, {'Content-type':'text/plan'});
     response.write('Sup bois!');
     response.end( );
    
    }).listen(7000);

    node 1stServer.js

    nano index.html

    <html>
    	<head>
    		<title>woah, it actually works</title>
    	</head>
    	<body>
    		<div style="width: 500; margin: auto;margin-top: 10%;text-align: center;font-size: 30;font-family: Arial;font-weight: 700;">
    			Hola Caracola!
    			<br><br>
    
    			<img src="https://media.giphy.com/media/vmv47p4zksWDC/source.gif" alt="">
    		</div>
    	</body>
    </html>PK 

