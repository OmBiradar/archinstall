# Setups

This section focuses on setting up various softwares

*Table of Contents*

1. Setting up Git & GitHub
2. How to install any application and setup it's desktop

## 1. Setting up Git & GitHub

Firstly, install Git using `sudo pacman -S git`. Now you would have to setup your user details so go on about doing:
```
git config --global user.name "<user_name>"
git config --global user.email "<user_email>"
ssh-keygen -t rsa -b 4096 -C "<user_email>" # Generate Key
eval "$(ssh-agent -s)" # Start the agent
ssh-add ~/.ssh/id_rsa # Add the key to the agent
cat ~/.ssh/id_rsa.pub # Copy paste this key in your GitHub SSH keys list
git config --global url."git@github.com:".insteadof "https://github.com/" # Switch from HTTP to SSH
```

Done, and now you should be able to push to github using your terminal under your id itself.


## 2. How to install any application and setup it's desktop

Download tar.gz file
Unzip it
move it to opt directory in root
create a symlink to the usr local bin folder
now create a .desktop file in /usr/share/applications/<name>.desktop
then edit the .desktop file in the following way
```
[Desktop Entry]

Type=Application

Name=Postman

Icon=/opt/Postman/app/resources/app/assets/icon.png

Exec=/opt/Postman/Postman

Comment=Postman Desktop App

Categories=Development;Code;
```
The above is for postman but you get the vibe.
