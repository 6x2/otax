# otax
hey, welcome to the whistle blow on the apparent "otax" exploit.

so, if you don't know what the "otax" exploit is, it's basically a discord token disclosure, only problem with this apparent "exploit" is, it is fake. <br>
there are 2 versions of "otax", two of which tell about different things, one is about discord WSG (websocket-gateway) analytics and the other is about the API endpoint known as "/science", which is fishy considering they are the same exploit. <br>

anyways, lets get into the solid evidence.
you can find both apparent [here](https://github.com/0x44F/otax) and [here](https://github.com/IRIS-Team/DiscordNoAuth0day), only made by 0x44F and one made by HellSec. <br>

first, i'll start with 0x44F "exploit" and then move onto HellSec's version:<br>
in his explaination, he claims to send a "specially crafted packet" to Discord's gateway server, but when you send any type of "specially crafted packet" to Discord's gateway, it will drop the connection and throw a 4001 event code, referring to the [Discord gateway documentation for closing events](https://discord.com/developers/docs/topics/opcodes-and-status-codes#gateway-close-event-codes) it states a 4001 event code is a "unknown opcode" aka a invalid payload, meaning it is impossible to send a "specially crafted packet". <br>
now going into his actual code, he has a variable called "src_ip" in his "WebSock" class which is never used once, but is still there for no apparent reason.
```python
class Websock:
  
    def __init__(self, src_ip, gateway, port: int):
        self.ip = src_ip
```
and in when he's calling the class "WebSock" with the parameter known as "gateway", he has a invalid DNS, as proven in the screenshot below.
```python
websocket = Websock("127.0.0.1","dga.gateway.discord.gg",512)
``` 
![invalid-dns](https://user-images.githubusercontent.com/74681745/132074577-52f89206-2414-43fe-9e55-d5bf08d2ac3a.png)
