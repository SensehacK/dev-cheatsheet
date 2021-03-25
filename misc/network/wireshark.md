# Wireshark


### Mac OS Issues

Wireshark - you don't have permission to capture on that device mac


According to User: gmale's answer on ask.wireshark.org, he solved his problem in this way and I'm sure that it could solve yours as well. It says:

1- Open Terminal

To see your exact user name (for me that was AliGht)

2- Type 'whoami'

enter image description here

3- execute the following commands:

cd /dev
sudo chown AliGht:admin bp*
and enter your computer password:

enter image description here

4- now type this command:

ls -la | grep bp
The last command will display a list of files such as:

enter image description here

5- Make sure all of them have your user name and admin as the user/group. For some reason, the last one didn't get assigned properly so I had to run the command:

sudo chown AliGht:admin bpf4
so the last command fixed my problem as you see in the last image:

enter image description here

Done!

If your WireShark is open then close it and open it again.

All credits of this tutorial goes to user gmale on ask.wireshark.org,

If you want to open WireShark always as administrator then take a look to another post which I created a shortcut for it via Applescript, and this is the only way which you can open the WireShark always as administrator even when you turn off/on your mac.

[SO](https://stackoverflow.com/questions/41126943/wireshark-you-dont-have-permission-to-capture-on-that-device-mac#42368892)