# Modifications compared to the original version:

As explained in this issue:
https://github.com/Hootrix/keyword_alert_bot/issues/29 信息显示为一行

The messages were shortened for a better overview as shown here:
![image](https://user-images.githubusercontent.com/665889/202410324-6b9b696f-27b0-4730-9491-6508fa30b89a.png)

The username was added for a faster way of communication with the poster of the thread:
![image](https://user-images.githubusercontent.com/665889/202411657-e3e75f5d-3447-41cf-b021-a3a385c94d3b.png)


config.yaml Some comments were added to better understand what should be edited:

![image](https://user-images.githubusercontent.com/665889/202410665-68ebbc74-ed29-47cc-9060-b03f86390c25.png)

![image](https://user-images.githubusercontent.com/665889/202412458-717e0601-ff61-42c0-9adb-e0912ec7e5e1.png)


# Here is how you get started:
## 1. Create account
### Create Telegram Account & API
https://my.telegram.org/apps

To open the api, it is recommended to use a newly registered Telegram account.

Get api_id, api_hash
![chrome_2022-08-08_11-04-17](https://user-images.githubusercontent.com/665889/183333531-ea69d6c8-b720-4efa-9c6e-fc31f2b5a252.png)

### Create BOT
Go to this adress in the telegram app or if you use web.telegram.com add in the search field:
https://t.me/BotFather
Then enter this in the chat to create a new bot: 
/start
/newbot
Enter bot name
Enter bot username

I think one of these should end with _bot. There are many manuals how to create a bot if you do not get along. 

Next copy token to access the HTTP API
![Telegram_2022-08-08_10-57-30](https://user-images.githubusercontent.com/665889/183334493-b6a906b4-bf0a-45ae-91be-ed1e5f2f2aa4.png)

## 2. Operating environment

# Preparing python related components
Based on Debian 11 environment. You can use any apt supported system, Ubuntu 22 will also work. Enter this to the SSH or bash console:
```
apt update
apt install -y pip 
pip install telethon peewee PySocks diskcache PyYAML asyncstdlib colorama text_box_wrapper
```

### Pull program files from GitHub
Get the compressed package address

![image](https://user-images.githubusercontent.com/665889/183339082-e409da96-6dfe-46e4-a592-9c434ebfd0bd.png)

Then enter this: 
```
cd 
wget -N https://github.com/crazypeace/keyword_alert_bot/archive/refs/heads/master.zip
unzip master.zip
cd keyword_alert_bot-master/
```

## 3. Edit config.yml

Modify the following fields
![Notepad3_2022-08-08_11-09-15-1](https://user-images.githubusercontent.com/665889/183334604-854fecfe-9499-4dd0-bfb2-b85a29a4baa8.png)

phone is the phone number of your new Telegram account.
username to your new Telegram account username

## 4. Start bot

You need python3 installed. You can then start the main component:
```
python3 ./main.py
```

The script window prompts you to enter a verification code, and at the same time, your new Telegram account receives a verification code
![image](https://user-images.githubusercontent.com/665889/183342317-6fd4e4a3-5670-4f97-b09c-11f8236024d8.png)

Enter this verification code into the script window

## 5. Autostart bot

### Run in the background using screen

There are several possibilities:
```
apt install -y screen
screen
python3 ./main.py
```

### Schedule tasks using crontab

```
crontab -e
```
When you run it for the first time, you will be prompted which editor to use. Just choose the one you like. Newbies recommend nano, which operates more like Win's notepad.

Enter the following line and save it

```
@reboot ( sleep 120 ; python3 /etc/keyword_alert_bot-master/main.py )
```

This means that after each reboot, wait 120 seconds before executing the following shell command.

# 🤖Telegram keyword alert bot ⏰


Used to remind channel/group keyword messages
If you want to subscribe to `group` messages, make sure that ordinary TG accounts do not require verification to join the group.
Principle: tg command line client to monitor messages, and use bot to send messages to subscribed users.

👉  Features：

- [x] Keyword message subscription: Send new message reminders based on set keywords and channels
- [x] Support regular expression matching syntax
- [x] Support multi-channel subscription & multi-keyword subscription
- [x] Support subscribing to group messages
- [x] Support message subscription of private channel ID/invitation link

  1. https://t.me/+B8yv7lgd9FI0Y2M1  
  2. https://t.me/joinchat/B8yv7lgd9FI0Y2M1 
  

👉 Todo:

- [ ] Private group subscriptions and reminders
- [ ] Full content preview of private channel message reminder
- [ ] Multiple account support
- [ ] Scan to exit useless channels/groups

# DEMO

http://t.me/keyword_alert_bot

![image](https://user-images.githubusercontent.com/10736915/171514829-4186d486-e1f4-4303-b3a9-1cfc1b571668.png)


# USAGE

## Normal keyword matching

```
/subscribe   免费     https://t.me/tianfutong
/subscribe   优惠券   https://t.me/tianfutong

```

## Regular expression matching

Use js regular grammar rules and wrap regular statements with /. Currently available matching modes: i, g

```
#Subscribe mobile phone model keyword: iphone x, exclude XR, XS and other models, and ignore case
/subscribe   /(iphone\s*x)(?:[^sr]|$)/ig  com9ji,xiaobaiup
/subscribe   /(iphone\s*x)(?:[^sr]|$)/ig  https://t.me/com9ji,https://t.me/xiaobaiup



```


