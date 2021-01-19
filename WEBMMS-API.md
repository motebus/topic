# List of API
## Command	Description
- MMS:	MMS class
- OpenMMS:	Open service of MMS
- SendMMS:	Send message to the other device
- StateMMS:	Get or set the state of MMS
- CallMMS:	Call function of the other device


## Function List

- OpenMMS:	WebMMS.OpenMMS()
- SendMMS:	WebMMS.SendMMS()
- StateMMS:	WebMMS.StateMMS()
- CallMMS:	WebMMS.CallMMS()


## MMS
### Input:
- app: name of app name
- wsurl: Url of web socket server
### Example:
```
let wsurl = 'boss.ypcloud.com:8081';
WebMMS = new MMS('myapp', wsurl);
```
## OpenMMS
### Input:
- regwsOK: callback after register to websocket server
- regdOK: callback after register to dCenter, no callback means that the app doesn't want to register to dCenter
- wsState: callback when websocket state changed
- rcveMsg: callback when websocket receive a message
### Example:
```
let WebMMS = new MMS('myapp',wsurl);
let  regwsOK = function(result){
    console.log('regWS OK %s', result.numUsers);
}
let wsState = function(result){
    console.log('WS error: %s', result);
}
let regdOK = function(result){
    console.log('regtoCenter: %s', result.ErrMsg);
} 
let rcveMsg = function(from, data){
    console.log('reve: from=%s, data=%s', from, JSON.stringify(data));    
}
WebMMS.OpenMMS( regwsOK, regdOK, wsState, rcveMsg );
```    
## SendMMS
### Input:
- ddn: ddn of device
- topic: topic of device
- data: data to be sent
- timeout (t1): timeout of send (null means default timeout)
- waitreply (t2): timeout of reply (null means default timeout)
- cb: callback of return
### Example:
```
let ddn = '>>ylobby';      
let topic = '';
let data = 'notify Hello 60 red 3';
let WebMMS = new MMS('myapp',wsurl);
WebMMS.SendMMS( ddn, topic, data, null, null
    function(result){
        console.log('sendMMS: result=%s', JSON.stringify(result));
    }
);
```
## StateMMS
### Input:
- cmd: command:
#### list of command:
- "nearby": get device nearby
- "search": search device
- "get": get state or information, depond on arg
- "set": get state or information, depond on arg and argv
- arg: argument of the command
- argv: value of the argument
- cb: callback of return
### Example:
nearby: query nearby device from
```
let WebMMS = new MMS('myapp',wsurl);
WebMMS.StateMMS( 'nearby', '', '', 
    function(devlist){
        console.log('nearby: list=%s', JSON.stringify(devlist));
    }
);
```
get device: get my device information
```
let WebMMS = new MMS('myapp',wsurl);
WebMMS.StateMMS( 'get', 'device', '',
    function(info) {
        console.log('get device: info=%s', JSON.stringify(info));
        // info: {DDN,EiOwner,EiName,EiType,EiTag,EiLog}
    }
);
```
set device: set my device information
```
let EiInfo = {"DDN":"","EiOwner":"","EiName","eiHello","EiType":".mc","EiTag:"#hello","EiLog":""};
let WebMMS = new MMS('myapp',wsurl);
WebMMS.StateMMS( 'set', 'device', EiInfo,
    function(result) {
        console.log('set device: result=%s', JSON.stringify(result));
    }
);
```
## CallMMS
### Input:
- ddn: ddn of device
- topic: topic of device
- func: function name of XRPC
- args: arguments of function
- timeout (t1): timeout of send (null means timeout)
- waitreply (t2): timeout of reply (null means timeout)
- cb: callback of return
### Example:
```
let ddn = '>>jLobby';
let topic = '';
let func = 'echo'      
let args = {"data":"Hello MMS"};
let WebMMS = new MMS('myapp',wsurl);
...
WebMMS.CallMMS( ddn, topic, func, args, null, null,
function(result){
    console.log('CallMMS: result=%s', JSON.stringify(result));
    }
);
```

## Error Code

| No |	Code    | Message           |
| -- | -------- | -----------       |
| 1	 | 0	    |OK                 |
| 2	 | -10501   |Invalid data       |
| 3	 | -10502	|Invalid command    |
| 4	 | -10503	|Stoken error       |
| 5  | -10504	|DC not link        |
| 6  | -10505	|Blank command      |
| 7	 | -10506	|Websocket not ready|


