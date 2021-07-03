Here are the instructions to reset your password:

1. Login to the HOOBS Box via SSH on your computer.

On MacOS use the Terminal app and type: ```ssh hoobs@hoobs.local```

Type yes to accept the certificate key then press enter. When prompted for password, type ```hoobsadmin```


On Windows, use Putty with the same credentials as above.


2. After successfully logging in, type this to reset the users file:  ```sudo rm -rf /home/hoobs/.hoobs/etc/access.json```

Press enter. There will be no output.


3. Type this to reboot the HOOBS Box: ```sudo reboot```


4. Allow 2-3 minutes for the HOOBS Box to reboot then go to the [HOOBS UI](http://hoobs.local) and create a new account.

This won't affect your plugins and accessories, only your user. 


**If you can't connect via SSH on Mac:**

---------------- MAC Host Key verification failed fix -----------------

1. Type in terminal app ```open /Users/cpasiak/.ssh/known_hosts```

2. Delete all content in the file

3. Save and close it

4. connect again via ssh
