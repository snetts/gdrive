You can use the open source Linux / Unix command line tool gdrive.

To install it:

Download the binary. Choose the one that fits your architecture, for example gdrive-linux-x64.

Copy it to your path.

sudo cp gdrive-linux-x64 /usr/local/bin/gdrive;
sudo chmod a+x /usr/local/bin/gdrive;
To use it:

Determine the Google Drive file ID. For that, right-click the desired file in the Google Drive website and choose "Get Link …". It will return something like https://drive.google.com/open?id=0B7_OwkDsUIgFWXA1B2FPQfV5S8H. Obtain the string behind the ?id= and copy it to your clipboard. That's the file's ID.

Download the file. Of course, use your file's ID instead in the following command.

gdrive download 0B7_OwkDsUIgFWXA1B2FPQfV5S8H
At first usage, the tool will need to obtain access permissions to the Google Drive API. For that, it will show you a link which you have to visit in a browser, and then you will get a verification code to copy&paste back to the tool. The download then starts automatically. There is no progress indicator, but you can observe the progress in a file manager or second terminal.

Source: A comment by Tobi on another answer here.

 

Additional trick: rate limiting. To download with gdrive at a limited maximum rate (to not swamp the network …), you can use a command like this (pv is PipeViewer):

gdrive download --stdout 0B7_OwkDsUIgFWXA1B2FPQfV5S8H | \
  pv -br -L 90k | \
  cat > file.ext
This will show the amount of data downloaded (-b) and the rate of download (-r) and limit that rate to 90 kiB/s (-L 90k).

# Authenticate

# remove the token file
rm ~/.gdrive/token_v2.json
# run the about subcommand to re-prompt you for authentication:
gdrive about
