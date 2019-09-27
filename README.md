fork from https://github.com/mmastrac/iterm2-zmodem

[中文教程](https://shaffer.cn/mac/%E8%A7%A3%E5%86%B3mac%E4%B8%8Biterm2%E4%BD%BF%E7%94%A8rz%E3%80%81sz%E5%AF%BC%E8%87%B4%E7%BB%88%E7%AB%AF%E5%8D%A1%E6%AD%BB%E7%9A%84%E6%83%85%E5%86%B5/)

ZModem integration for iTerm 2
------------------------------

This script can be used to automate ZModem transfers from your OSX desktop to a server that can run `lrzsz` (in theory, any machine 
that supports SSH), and vice-versa.

The minimum supported iTerm2 version is 1.0.0.20120108

Troubleshooting
---------------

 * Sending a directory may fail: this is a known issue
 * If you are using `tmux` or some other terminal multiplexer, try using the `-e` option to `sz` and/or `rz` on your server to force escaping of more characters during transmission.

Setup
-----

0. Install lrzsz on OSX: `brew install lrzsz`
1. Save the `iterm2-send-zmodem.sh` and `iterm2-recv-zmodem.sh` scripts in `/usr/local/bin/`
2. Set up Triggers in iTerm 2 like so:

<pre>
    Regular expression: rz waiting to receive.\*\*B0100
    Action: Run Silent Coprocess
    Parameters: /usr/local/bin/iterm2-send-zmodem.sh
    Instant: checked

    Regular expression: \*\*B00000000000000
    Action: Run Silent Coprocess
    Parameters: /usr/local/bin/iterm2-recv-zmodem.sh
    Instant: checked
</pre>

To send a file to a remote machine:

1. Type `rz` on the remote machine
2. Select the file(s) on the local machine to send
3. Wait for the coprocess indicator to disappear

The receive a file from a remote machine

1. Type `sz filename1 filename2 … filenameN` on the remote machine
2. Select the folder to receive to on the local machine
3. Wait for the coprocess indicator to disappear

Future plans (patches welcome)

 - Visual progress bar indicator