This Project was written so when you call a client either hosted on a raspberry pi debian/ubuntu machine like me using a proxmox lxc container, it plays a random .wav file from a folder.
My wav files are named 0922-2.wav through 0922-26.wav in the extensions folder, do not include .wav extension.


Step 1: update your repositories
sudo apt update && sudo apt upgrade -y

Step 2: install asterisk
sudo apt install asterisk

Step 3: edit the sip.config file to work in your case. Here is mine with redacted info
You'll need to update the USERNAME, PASSWORD, and SERVER_ADDRESS to match your enveronviment in my example extensions.conf file.
sudo nano /etc/asterisk/sip.conf

Step 4: add wav files to the wav folder. I used winSCP
the .wav file must be a sample rate of 8000 Hz and mono audio.
most likley your user sounds will be in the sounds/en filder located in the en directory. make a wav directory.
cd /usr/share/asterisk/sounds/en/
sudo mkdir wav

Step 5: edit the extensions.conf files dialing plans
You'll need to update based on your file names in your wav folder. you can use my example extensions.conf as my wav filenames are 0922-2 through 0922-26.
sudo nano /etc/asterisk/extensions.conf

Step 6: restart asterisk
sudo asterisk -rx "reload"

Troubleshooting from what i learned
1. If you call into the extension & it's a busy signal it's probably the sip.conf issue
2. if you call into the extension & it hangs up or you hear anything other than your wav files then it's your extensions.conf file.
3. to pull up live asterisk logs while you test, run
sudo tail -f /var/log/asterisk/messages
