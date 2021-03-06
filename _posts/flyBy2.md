# What is this for

Learning _web development_ in this day and age is something that lots of people are already doing, but we only know half of it. We only dive into the client-side end of the deal, so we know how to use HTML and javascript, but server-side is never mentioned.

So this is what this is for, what is a server, what it does and why should you even think about them.

# Let the nerds take care of that.

To that I would say no, a server is basically a computer somewhere storing information that when requested, gets 'served' to the client. That is basically how the internet works, A bunch of computers in places giving you stuff when you ask for it. 

A fearly easy action that besides its value most people that work in projects that require a service like this don't really know the basics of it.

So here we are, trying to tell you what this is and how to set up an eviroment for you to play around with all this. 

# Digital Ocean

Either you left cause you don't care about this or you wanna work in this soon to be nightmare.

So lets dive into [digitalOcean](https://www.digitalocean.com) (get it?).

## droplets.

A droplet is virtual computer. An emulation of an actual computer set up inside a real much more powerful machine. this allows getting your hands into a computer very fast and easily. In this case one with a public IP and and a easy access from anywhere. This allows to create servers and to put them up in no time.

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

 **_`curl`_** _ is a tool to transfer data from or to a server that uses the most used protocols in webservers._ 

    curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh

Once we get this script we run it. This will prep the system so we can install **node** normally with **`apt-get`** **.** 

 _`**apt-get**`_ _** **_ _is the package manager for linux._ 

    sudo bash nodesource_setup.sh

    sudo apt-get install nodejs

Now that node is installed we can proceed to build the first server but to make sure everything you download with npm works, is better to also get the **build essential** package.

    sudo apt-get install build-essential

# 1stServer.js

Everything is on place to start creating the server, first we need a place where to keep the server file, therefore we need a directory, to do that we use the command **`mkdir`** (make directory)

    mkdir 1stServer

Now we can start adding the contents, like the server file, to do that, we have to enter the directory, that is done using the **`cd`** command.

 _Is good to know that you can autocomplete the prompt you are writing by using tab after a X amount of letters;_ 

 _i.e. if you are writing "_ **_1stServer.js"_** _ you can write _ **_1_** _ and then tab, that would complete the prompt due not being any other files starting with a _ _**1 **_ _in the current directory. This might change if there's a file called _ **_"1stFile.html"_** _, if you just write _ **_1_** _, the prompt is going to give you all the files that start with _ **_1._** _ That means that If you write "_ **_1stF"_** _ then the autocomplete will be _ **_"1stFile.html"_** 

    cd 1stServer

Now that you are inside the directory, you can create the server file. Using the **touch** command

    touch 1stServer.js

To edit the file we just created we use **`nano`** 

 **_`nano`_** _ is one of multiple text editors inside the command line, is one of the easiest to get used to and works in a very similar way than regular text editor. Others might be _ **_emacs_** _, and _ _**vim.**_ _ _ 

    nano 1stServer.js

When using node most of the time you are using certain **modules** , you make use of these modules by calling them. you do that by creating a **variable** that calls a **`require`** for the module **`'http'`** that has the functions to create a http server.

After that we **create the server** and tell it what to do. in this case we are just sending a string to be displayed when you connect.

In the last line we are setting the port where to set all this up.

 _the _ **_port_** _ is the location where the server _ **_listens_** _ for a _ **_client_** _ to come up when connecting, so if you connect to a different one, the server won't provide anything, but if you go to the correct place, the server knows what you are looking for and gives it to you._ 

    var http = require('http'); // we call the module
    
    http.createServer(function(req, res){ [//](//we) server is set up to request and respond 
     res.writeHead(200, {'Content-type':'text/plan'}); // we set the type of response, to plain text 
     res.write('Sup bois!'); // message to be sent 
     res.end( ); // we are done with the response 
    
    }).listen(7000); // port where to listen for requests

To exit **`nano`** , there is a list of commands right in the bottom of the editor, to leave we press _ctrl+x_ , confirm or change the name and exit.

To try out if the file works, we run it using the command ' **`node`** **'** and the name of the file. To check if it's working go to ( **_whatever.is.your.ip:7000 _** ) in your web browser.

    node 1stServer.js

If everything worked out, you should see something like this:

![](https://static.notion-static.com/9d9b6468421f47d4b434b433e34873eb/Screen_Shot_2017-10-26_at_14.54.36.png)

---

# 2ndServer.js

Here we are doing the same as before, but this time is a bit more complex. this is just a basic website that allows you to navigate between links as you would in any static html page.

    var http = require('http');
    var fs = require('fs');
    var httpServer = http.createServer(requestHandler);
    var url = require('url');
    
    httpServer.listen(7000);
    
    function requestHandler(req, res) {
    
     var parsedUrl = url.parse(req.url);
     console.log("The Request is: " + parsedUrl.pathname);
    
     fs.readFile(__dirname + parsedUrl.pathname,
     function (err, data) {
     if (err) {
     res.writeHead(500);
     return res.end('Error loading ' + parsedUrl.pathname);
     }
     res.writeHead(200);
     res.end(data);
     }
     );
    }

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
    </html>

    sudo npm install -g pm2

    pm2 start 2ndServer.js
    
    pm2 stop 2ndServer.js
    
    pm2 restart 2ndServer

    pm2 list
  
    pm2 info 2ndServerPK 


