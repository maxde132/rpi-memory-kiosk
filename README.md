# Kiosk Display Setup with Pi 4 and a Display

# What is this?
- This is a kiosk where the pi shows weater data in the foreground and a picture (that changes every few secs) in the background.
- This is a solution to hidng the cursor in rpi-os desktop
- This is an amazing mother's day gift (if used with childhood pics)


# Insturctions
File Structure:
- Place kiosk.html in your home directory.
- Store images inside a directory called "memories" (same parent directory as kiosk.hmtl), ensuring they are named numerically from 1.JPEG to highestnumber.JPEG (ex. 13.JPEG).

Configuration:
- Update the totalImages constant in kiosk.html to match the actual image count:
  (ex. const totalImages = 10;)

- Update the weather API location:
  const url = `https://api.open-meteo.com/v1/forecast?latitude=INSERTLATITUDE&longitude=INSERTLONGITUDE&current_weather=true`;
  
  (ex. `https://api.open-meteo.com/v1/forecast?latitude=1.2345&longitude=3.14159`)

Running the Kiosk:
- To start the kiosk manually, run:
  chromium-browser --kiosk --noerrdialogs --no-sandbox file:///home/INSERTUSERNAME/kiosk.html

Auto-Start on Boot:
- Edit the AutoStart file:
  nano /etc/xdg/lxsession/LXDE-pi/AutoStart
- Add these lines:

- 
  `@unclutter -idle 0.1 -root
  @xset s noblank
  @xset s off
  @xset -dpms
  @chromium-browser --noerrdialogs --disable-infobars --no-sandbox --kiosk file:///home/INSERTUSERNAME/kiosk.html`

Fix Mouse Cursor Issues:
- Add the following to the end of your crontab:
  @reboot sleep 12 && startx -- -nocursor
# Have fun! 🚀
