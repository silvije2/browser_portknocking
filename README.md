# browser_portknocking

Portknocking with javascript from browser

# Why?

Because. Simple javascript knocking was not good enough for me because of websocket initial connection opening too long timeout

Http knocking seems to work despite of network error and warnings about blocked content because of CORS request policies

# Usage

You can use websocket or http knocking functions

Edit xPortKnock functions to achieve wanted portknocking sequence, timeout is in ms (give at least 200ms)

```
function wsKnock(ip,port,timeout){
    return new Promise(function(resolve, reject){
        //var sock = new WebSocket('ws://'+ip+':'+port);
        var sock = new WebSocket('wss://'+ip+':'+port);
        var timer = setTimeout(function(){
            reject(new Error("WebSocket timeout!"));
            sock.close();
        }, timeout);
    });
}

function httpKnock(ip,port,delay) {
    setTimeout(() => {
        var sock = fetch('https://'+ip+':'+port);
        console.log('Knocked: '+ip+':'+port);
    }, delay);
}

async function wsPortKnock(ip){
    wsKnock(ip,10001,200).then(function(){});
    wsKnock(ip,10002,500).then(function(){});
    wsKnock(ip,10003,900).then(function(){});
    wsKnock(ip,10004,1300).then(function(){});
    wsKnock(ip,10008,1700).then(function(){});
    wsKnock(ip,10009,2000).then(function(){});
}

async function httpPortKnock(ip){
    httpKnock(ip,20095,200);
    httpKnock(ip,20091,500);
    httpKnock(ip,20092,900);
    httpKnock(ip,20097,1300);
    httpKnock(ip,20093,1700);
    httpKnock(ip,20094,2000);
}

window.onload = function(){
    //httpPortKnock(ip);
    wsPortKnock(ip);
}
```

## Authors

* **jfriend00** [StackOverflow](https://stackoverflow.com/users/816620/jfriend00) modified from his example
* **Silvije2** [Github](https://github.com/silvije2/)

