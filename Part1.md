# commands

1. mount

2. nl

3. ufw

4. sort

5. column

6. yes

7. uniq

8. awk

9. convert

10. ffmpeg

      

## mount

```bash
~ mount --bind ~/my-new-website /var/www
```

It could resemble `ln`, but it's quite different. The above command basically binds a folder in your home dir to `/var/www` which nginx has full access

## nl

`nl` adds line numbers to beginning of lines. It skips empty lines by default, unlike `cat -n` or `less -N`;

You can optionally apply more conditions such as counting lines matching regular expressions.

```bash
~ nl test.py
     1	import time
     2	string = 'abcde?'
       
     3	t0 = time.time()
     4	print(string.endswith('?'))

```

## ufw

Uncomplicated Firewall (ufw) makes firewall configuration easier than exitting Vim. For example, you can allow a specific port to be accessible by any IP;

```bash 
~ ufw allow 22
```

If you want to allow only specific IPs:

```bash 
~ ufw allow from $trustedIP to any port 22
```

## sort

lets start sorting things

```bash
~ cat abc       
unix
omg
123
zfc
abc
pqr
wq
x
```

now lets try sort 

```bash
~ sort abc    
123
abc
omg
pqr
unix
wq
x
zfc
```

## column



```bash
~ cat help 
start: Start development mode.
stop: Stop development mode.
compile: Compile the binary
```

It's hard to read that! We can add some spacing with `column`:

```bash
~ column -t help
start:    Start    development  mode.
stop:     Stop     development  mode.
compile:  Compile  the          binary
```

its all in columns but next one is better 

```
~ column -t -s':' help
start     Start development mode.
stop      Stop development mode.
compile   Compile the binary
```

## yes

```bash
~ yes | pacman -S wtf
```

## uniq

Filters duplicate lines as its name suggests. Let's create a file with duplicate lines first

```bash
~ cat > file.txt
foo
bar
foo
qux
foo
qux
```

We can output it without the duplicates, adding counts to the beginning of line but only the next dublicates 

```bash
~ sort file.txt | uniq -c
1 bar
3 foo
2 qux
```

## awk

Awk is a data manipulation language, and it's probably one of the most powerful command-line tools ever. In this post I'll only cover basic use cases of it, for example, let's say we want to get the list of disks in our system

```bash
~ lsblk -l
NAME MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda    8:0    0 238.5G  0 disk 
sda1   8:1    0   450M  0 part 
sda2   8:2    0   100M  0 part /boot/efi
sda3   8:3    0    16M  0 part 
sda4   8:4    0  29.3G  0 part 
sda5   8:5    0 200.8G  0 part /
sda6   8:6    0   7.9G  0 part [SWAP]
```

This looks too verbose to my eyes. I only want to see the name of the disk, and the size. `awk` can help me

```bash
~ lsblk -l | awk '{print $1,$4}'
NAME SIZE
sda 238.5G
sda1 450M
sda2 100M
sda3 16M
sda4 29.3G
sda5 200.8G
sda6 7.9G
```

above, we asked awk to select & print 1st and 4th columns with `'{print $1,$4}'`.

## convert

`convert` is a powerful command-line image manipulation utility. You can get simple tasks such as converting between formats done easily, but it does more than that.

Here is an example; we downloaded a high resolution wallpaper and want to scale it to 2000px, keeping its original proportions.

```bash convert -scale 2000 ~/wallpaper.jpg  /tmp/wallpaper.png
~ convert -scale 2000 ~/wallpaper.jpg  /tmp/wallpaper.png
```

 Let's do something more complicated than just resizing; we'll add a transparent & black overlay on top of the wallpaper, and write a Goethe quote in the middle, just to make it look cool.

```bash
~ convert ~/wallpaper.jpg \
            -scale 1500 \
            -fill black -colorize 50% \
            -font System-San-Francisco-Display \
            -fill "#ffffff33" \
            -gravity center -pointsize 30 -annotate +0-200 'A man sees in the world what he carries in his heart. — Goethe' \
            result.jpg
```

## ffmpeg

I remember spending hours looking for a simple audio or video editing tool when I was not using Linux. `ffmpeg` is one amazing command that can be used for editing both sound and video files.

For example, you could trim an mp3 file with it:

```bash
~ ffmpeg -i input.mp3 -ss 00:00:20 -to 00:00:40 -c copy output.mp3
```

Above command will simply create a new mp3 file from between 20 (`--ss`) and 40 (`--t`) seconds. You could apply the same command into a video file, too

`ffmpeg` can record video, too. If you wanted to record your screen to share with others, here is the command to do that;

```bash
~ ffmpeg -video_size 1200x600 -f x11grab -i :0.0 output.mp4
```

Let's explain the parameters above:

- `-f x11grab` selects the encoder. This is required.
- `-i :0.0` selets the X server $DISPLAY, this is also required.

Optionally, we can choose a specific x/y value instead of the left/top of the screen `-i :0.0+250,150`

How would you know the coordinate of where you want to point left/top of the video though ? `xdotool` has an option to output mouse location

```bash
~ xdotool getmouselocation --shell
X=2096
Y=1353
```

one can also use slop for that

```bash
~ slop                 
860x540+464+245
```

basically it lets you select a region on your screen and outputs the region
