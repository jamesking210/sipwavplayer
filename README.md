### This Project was written so when you call a client either hosted on a Proxmox lxc or raspberry pi debian/ubuntu machine. it plays a random .wav file from a folder.
I'm use Proxmox and Helper-Scripts https://tteck.github.io/Proxmox/#ubuntu-lxc
### Optional Step depending on your environment. RUN ADVANCED SETUP AND RENAME LXC & ENABLE SSH

Youtube How-To Video: https://www.youtube.com/watch?v=VVNJMFVjGGI
Product inspiration for this project: https://www.youtube.com/watch?v=OGLVeeOa844

```bash
bash -c "$(wget -qLO - https://github.com/tteck/Proxmox/raw/main/ct/ubuntu.sh)"
```

*My wav files are named 0922-2.wav through 0922-26.wav in the extensions folder, do not include .wav extension.

Step 1: update your repositories
```bash
sudo apt update && sudo apt upgrade -y
```
Step 2: install asterisk
```bash
sudo apt install asterisk -y
```
Step 3: edit the sip.config file to work in your case. Here is mine with redacted info
You'll need to update the USERNAME, PASSWORD, and SERVER_ADDRESS to match your enveronviment in my example sip.conf file.
```bash
sudo nano /etc/asterisk/sip.conf
```
Step 4: add wav files to the wav folder. I used winSCP
the .wav file must be a sample rate of 8000 Hz and mono audio.
most likley your user sounds will be in the sounds/en folder located in the en directory. make a wav directory.
```bash
cd /usr/share/asterisk/sounds/en/
```
```bash
sudo mkdir wav
```
### ** UPLOAD FILES - Use something like WinSCP to add files to /usr/share/asterisk/sounds/en/wav folder
to get the machine's ip:
```bash
ip a
```
Step 5: edit the extensions.conf files dialing plans
You'll need to update based on your file names in your wav folder. you can use my example extensions.conf as my wav filenames are 0922-2 through 0922-26. Please edit line 3 with your DID number. If you have more than one DID, copy and paste line 3 and put the other DIDs in there.
```bash
sudo nano /etc/asterisk/extensions.conf
```
Step 6: restart asterisk
```bash
sudo asterisk -rx "reload"
```
Troubleshooting from what I've learned
1. If you call into the extension & it's a busy signal it's probably the sip.conf issue
2. if you call into the extension & it hangs up or you hear anything other than your wav files then it's your extensions.conf file.
3. to pull up live asterisk logs while you test, run
```bash
sudo tail -f /var/log/asterisk/messages
```
```bash
sudo asterisk -rvvvvv
```
Sites that helped:
https://cloudconvert.com/mp4-to-wav
https://tteck.github.io/Proxmox/#ubuntu-lxc
Affiliate link to VOIP Service (we both earn $10 when you deposit $15 and 1st call is made):
https://voip.ms/en/invite/MzE5NzAy
