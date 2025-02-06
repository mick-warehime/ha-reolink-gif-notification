# Reolink Video Notifications for Home Assistant

Forked from https://github.com/jterrace/ha-reolink-rich-notifications


1. Install ffmpeg

I tried doing this with various add-ons but ended up launching the terminal add-on and just installing with `apk`.

```
apk update

apk add ffmpeg
```

2. Teach HA to convert a set of images to a video 

The Studio Code Server add-on is very nice for these steps [link](https://community.home-assistant.io/t/home-assistant-community-add-on-visual-studio-code/107863)

2a. Create a new directory /config/scripts/

2b. Copy the following contents into a new file called create_mp4.sh in the new directory

```
ffmpeg -f image2 -framerate 2 -i "$1%02d.jpg"  -c:v libx264 -pix_fmt yuv420p "$1.mp4"
``` 

2c. Add the following line to configuration.yaml

```
shell_command:
  create_gif: /bin/bash /config/scripts/create_mp4.sh "{{ arguments }}"
```

3. Add this blueprint as a new blueprint

a. Use HACS to add a custom repository, or

b. Copy this file to the blueprints directory