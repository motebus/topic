# List of SmartScreen API
| # | Command |	     Description         |
| - | ------- | ------------------------ |
| 1 | Drop | Show image or video on screen |
| 2 | Notify | Show a notification message |
| 3 | Toast | Show a toast message |
| 4 | Marquee |	Show a marquee text |
| 5 | Text | Show text to screen |
| 6 | App |	Show a website on screen |
| 7 | Youtube |	Show a youtube program on screen |
| 8 | Touch	| Control sscreen |
| 9 | Status | Show status of sscreen |



# Use API 
## Use xMsg to control SmartScreen
### Function: xmsg.send()
### Paramters:
- DDN: "yview"
- Target: ""
- Data: (command of smartscreen)

## Use xRPC to control SmartScreen
### Function: xrpc.call()
### Parameters:
- DDN: "yview"
- Target: ""
- Func: "cmd"
- Data: (command of SmartScreen)

## Command Format
1.	CLI: Command line command, type is string.
2.	JSON: {"cmd":"drop",…}
 
# Command
## Drop
### CLI:
drop (url) (duration) (frame) (animate) (animate duration) (play mode)
### JSON:
{"cmd":"drop","type":"url","src":["(url1)","(url2)"],"duration":"(duration)","frame":"(frame)","animate":"(animate)","aniduration":"(animate duration)","pmode":"(play mode)" ,"bgcolor":"(background color)"}
### Example:
Example 1
```
drop http://cdn.ypcall.com/miki/yp/djdemo/sugar.mp4 30 main
```
Example 2
```
drop http://cdn.ypcall.com/miki/yp/djdemo/sugar.mp4 30 main fade 2 loop
```
Example 3
```
{"cmd":"drop","type":"url","src":["http://cdn.ypcall.com/miki/yp/djdemo/sugar.mp4"],"duration":"0","frame":"t2","animate":"fade","aniduration":" 2","bgcolor":"white","pmode":"loop"}
```
Note:
1.	duration: unit is second, 0 means play to end
2.	frame: can be main, t1, t2, t3, or t4
3.	CLI use "," to separate multiple URLs.
4.	animate: can be delay, fade, slide, left, right
5.	animate duration: unit is second.
6.	pmode: can be loop or random

## Notify
### CLI:
notify (message) (duration) (color) (size)
### JSON:
{"cmd":"notify","msg":"(message)","duration":"(duration)","color":"(color)":"size":"(size)"}
### Command Example
```
notify HelloWorld! 30 black 3
```
```
notify "Hello World!" 30
```
```
{"cmd":"notify","msg":"HelloWorld!","duration":"30","color":"lime":"size":"4"}
```
Note:
For CLI, if has space in message, use "" to enclose the message string.
Message Keyword:
1. (%time): current time.
2. (%time#yyyy/mm/dd hh:nn:ss): current time with format

## Toast
### CLI:
toast (message) (heading) (icon) (transition) (duration)
### JSON:
{"cmd":"toast","msg":"(message)","heading":"(heading)","icon":"(icon)":"transition":"(transition)","duration":"(duration)"}
### Command Example
```
toast HelloWorld! Welcome info plain
```
```
{"cmd":"toast","msg":"Hello World!","heading":"Welcome","icon":"info","transition":"plain","duration":"5"}
```
Note:
1.	For CLI, if has space in message, use "" to enclose the message string.
2.	Icon: can be info, waring, error and success
3.	Transition: can be plain, fade and slide
4.	duration: unit is second, >= 1

## Marquee
### CLI:
marquee (message) (duration) (color) (size)
### JSON:
{"cmd":"marquee","msg":"(message)","duration":"(duration)","color":"(color)":" size":"(size)","bgcolor","(background color)"}
### Command Example:
```
marquee HelloWorld! 30 black 3
```
```
marquee "Hello World!" 30
```
```
{"cmd":"marquee","msg":"Hello World!","duration":"30","color":"lime","size":"4","bgcolor":"lime"}
```
Note:
For CLI, if has space in message, use "" to enclose the message string.

## Text
### CLI:
text (text) (duration) (color) (size) (background color) (text alignment) (frame) (animate) (animate duration)
### JSON:
{"cmd":"text","msg":"(text)","duration":"(duration)","color":"(color)","size":"(siz e)","bgcolor":"(background color)","align":"(text alignment)","frame":"(frame)","animate":"(animate)","aniduration":"(animate duration), "bgcolor":"(background color)"}
### Command Example:
```
text HelloWorld! 30 black 3 white left text
```
```
text "Hello World!" 30 lime 4 yellow center main
```
```
{"cmd":"text","msg":"Hello World! ","duration":"30","color":"lime":"size":"4","bgcolor":"white","align":"left","frame":"main","animate":"slide","aniduration":"1","bgcolor":"red"}
```
Note:
1.	For CLI, if has space in message, use "" to enclose the message string.
2.	Align can be center, left or right
3.	Frame can be text, main, t1, t2, t3, or t4.
4.	duration: unit is second, 0 means play to end
5.	animate: can be delay, fade, slide, left, right
6.	animate duration: unit is second.

## APP
### CLI:
app (url) (duration) (frame)
JSON:
{"cmd":"app","url":"(url1)","duration":"(duration)","frame":"(frame)"}
### Command Example:
```
app http://www.ypcloud.com 30 main
```
```
{"cmd":"app","url":"http://www.ypcloud.com","duration":"0","frame":"t2"}
```
Note:
1.	duration: unit is second, 0 means play to end
2.	frame can be main, t1, t2, t3, or t4.


## Youtube
### CLI:
youtube (search) (duration) (frame) (play mode)

### JSON:
{"cmd":"youtube","search":"(search string","duration":"(duration)","frame":"(frame)","pmode":"(play mode)"}

### Command Example:
```
youtube sugar 30 main loop
```
```
{"cmd":"youtube","search":"sugar","duration":"0","frame":"t2","pmode":"loop"}
```

Note:
1.	duration: unit is second, 0 means play to end
2.	frame: can be main, t1, t2, t3, or t4
3.	pmode: can be loop or random

## Touch
### CLI:
touch (option) (value)

### JSON:
{"cmd":"touch","option":"(arg) ","value":"(argv)"}

### Command Example:
```
touch playnext
```
```
{"cmd":"touch","option":"playnext","value":""}
```
### Touch command table

| # | option | description |
| - | ------ | ----------- |
| 1	| "playnext" | play next media |
| 2	| "playprev" | play previous media |
| 3	| "playfirst" | play first media |
| 4	| "playlast" | play last media |
| 5	| "playlist" | get playlist |
| 6	| "playindex" | play media by index of playlist |
| 7 | "chnext" | play next channel |
| 8	| "chprev" | play previous channel |
| 9	| "chfirst" |	play first channel |
| 10 | "chlast" |	play last channel |
| 11 | "play" | play media |
| 12 | "pause" | play pause |
| 13 | "stop" | play stop/pause |
| 14 | "mute" | mute |
| 15 | "unmute" |	unmute |
| 16 | "volup" | volume up 10% |
| 17 | "voldown" | volume down 10% |
| 18 | "console" | console control command |
| 19 | "setting" | setting control command |
| 20 | "eisetting" | setting process command |

### Touch command value description
| # | option | value | description |
| - | ------ | ----- | ----------- |
| 18-1 | "console" | "onoff" |	console on/off |
| 18-2 |  | "clear"  |console clear |
| 18-3 |  | "scrollup" | console scroll up |
| 18-4 |  | "scrolldown" | console scroll down |
| 18-5 |  | "logs" | console last 20 logs |
| 18-6 |  | "remote" | remote console on/off |
| 19 |	"setting" | "onoff" |	setting page on/off |
| 20-1 | "eisetting" | {name,tag,loc} |	setting ei information |
| 20-2 |  | "get" |  get ei information |


## Status

### CLI:
status (arg) (argv)

### JSON:
{"cmd":"status","option":"(arg) ","value":"(argv)"}

### Example:
```
1.	status frame main
2.	{"cmd":"status","option":"frame","value":"main"}
```
### Touch command table
| # | option | value | description |
| - | ------ | ----- | ----------- |
| 1 | "frame" | "use" |	Frames usage summary |
| 2 | "frame" | "main" | Frame usage of main |
| 3	| "ver" |  | The version of software |
| 4	| "devinfo" | | Edge setting |

## Dj
### CLI:
dj (arg) (argv)

### JSON:
{"cmd":"dj","option":"(arg) ","value":"(argv)"}

### Dj command table

| #	| option | value | description |
| - | ------ | ----- | ----------- |
| 1	| "logo" | [url] | Change logo to the url |
| 2	| "enable" | [job name] *(note 1)* | Enable the job |
| 3 | "disable" |	[job name] *(note 1)*| Disable the job |
| 4	| "kiosk" | "true" or "false" |	Kiosk mode on or off |
| 5	| "startcmd" | [{cmd object}] *(note 2,3)* | Add dj command when startup |
| 6 | "restart" |	 | Restart web page |

Note: 
1.	default job: name is "default", will execute the last drop command when startup.
2.	Command format: 
[{"cmd":[{"cmd":""}],"delay":""}]
3.	Command example:
[{"cmd":{"cmd":"drop","type":"url","src":["https://www.ypcloud.com"]},"delay":"5"}]
[{"cmd":{"cmd":"droplast"},"delay":"5"}]

### Command Example:

```
Dj logo http://cdn.ypcall.com/miki/ypcloud/jujue.png
```
```
Dj enable default
```
```
Dj kiosk true
```
```
{"cmd":"dj","option":"logo","value":" http://cdn.ypcall.com/miki/ypcloud/jujue.png "}
```
```
{"cmd":"dj","option":"enable","value":"default"}
```
```
{"cmd":"dj","option":"startcmd","value":[{"cmd":{"cmd":"drop","type":"url","src":["https://www.ypcloud.com"]},"delay":"5"}]}
```
```
{"cmd":"dj","option":"startcmd","value":[{"cmd":{"cmd":"droplast"},"delay":"5"}]}
```
```
{"cmd":"dj","option":"restart","value":""}
```
## Error Code

| No | Code | Message |
| -- | ---- | ------- |
| 1 | 0	| OK |
| 2	| -10699 | smartscreen: error |
| 3	| -10601 | smartscreen: invalid data |
| 4	| -10602 | smartscreen: invalid command |
| 5 | -10603 | smartscreen: process error |
| 6 | -10604 | smartscreen: busy |


