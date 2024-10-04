This Project was written so when you call a client either hosted on a raspberry pi debian/ubuntu machine like me using a proxmox lxc container, it plays a random .wav file from a folder.

Step 1: update your project repositories
sudo apt update && sudo apt upgrade -y

Step 2: install asterisk
sudo apt install asterisk

Step 3: edit the sip.config file to work in your case. Here is mine with redacted info
sudo nano /etc/asterisk/sip.conf

Step 4: add wav files to the wav folder. I used winSCP
the .wav file must be a sample rate of 8000 Hz and mono audio.
most likley your user sounds will be in the sounds/en filder located in the en directory. make a wav directory.
cd /usr/share/asterisk/sounds/en/
sudo mkdir wav

Step 5: edit the extensions.conf files dialing plans
sudo nano /etc/asterisk/extensions.conf

Step 6: restart asterisk
sudo asterisk -rx "reload"
