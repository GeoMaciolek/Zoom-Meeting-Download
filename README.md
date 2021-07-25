# Zoom-Meeting-Download

## Overview

> Note 2021-07-25: This is a fork of [tribloom/Zoom-Meeting-Download](https://github.com/tribloom/Zoom-Meeting-Download) adding features & cleanup. (Undecided if I'll try to get it merged!) I'm in the process of converting it to use jwt keys etc. This is very much a a "use at your own risk" tool, and I'd advise against using it if you're not familiar with python and the shell. --GMaciolek

Note: You must create a "logs" directory under scripts location or you will get an error. You will need to have a OAuth credentials from Zoom in order to run the script, not a user's key and secret. Instructions for Zoom Oauth are found at https://marketplace.zoom.us/docs/guides/build/oauth-app. You may want/need to adjust line 553 (`directory = "/srv/app_bconnsync_aux0/" + args["email"] + " Zoom recordings"+date_string`) to fit your OS and directory structure.

Download Zoom cloud recordings and transfer them to Google drive using `rclone`

## Usage

### Install Dependencies

Use `pipenv` to create a virtual environment, or otherwise use pip to manage the requirements from `Pipfile`

```
$ pipenv shell
$ pipenv install
```

### Run Application

```
$ mkdir logs
$ python zoom_meeting_download.py

python zoom_meeting_download.py -s <settings_file> -e <email> -f <from> -t <to>
Options:
  -e email     download this Zoom user's recordings
  -f from      the date from which to download recordings, format yyyy-mm-dd, if not provided defaults to 2019-09-26
  -s settings  load settings from file
  -t to        the date from which to download recordings, format yyyy-mm-dd, if not provided defaults to today's date
  ```

## Troubleshooting

`AttributeError: 'str' object has no attribute 'decode':`
There appears to be an issue with PyJWT that causes this error in newer versions of the library. See https://github.com/jazzband/djangorestframework-simplejwt/issues/346 for details. You can run 'pip freeze' to see the installed version of PyJWT. To downgrade library verions:
```
pip uninstall PyJWT
pip install --upgrade PyJWT==1.7.1
```
