#XMPP协议#

* ###XML Stanzas###

* ####每个客户端用JID来作为身份标识 `[user"@"]domain["/"resource]`####

* ####示例####


```xml
    <stream:stream>
    
    ...
    
    <presence>  
    <show/>  
    </presenece>

    <message to='foo'>
    <body/>
    </message>
    
    <iq to='bar'>
    <query/>
    </iq>

    ...
    
    </stream:stream>
```

* ####XML Stanzas通用属性####
    * `from` -> 源JID（服务器一般不信任，一般根据连接状态自动获取）
    * `to` -> 目的JID
    * `type` -> 
    * `id` -> 服务器和客户端之间的标识符

* ####stream结构####
    * Client to Server

      ```xml
      <stream:stream
          to="example.com"
          xmlns="jabber:client"
          xmlns:stream="http://etherx.jabber.org/streams"
          version="1.0">
      ```
    * Server to Client      


      ```xml
      <stream:stream
          from="example.com"
          id="someid"
          xmlns="jabber:client"
          xmlns:stream="http://etherx.jabber.org/streams"
          version="1.0">
      ```
      
    * Close Client
    
      ```xml
      </stream:stream>
      ```
    * Close Server
    
      ```xml
      </stream:stream>
      ```
 
* ####presence结构####

```xml
    <presence
        from="jackson@gmail.com"
        to="jimmy@msn.com"
        type="unavailable"/>
```
    * `type`可选参数：
        * available：上线
        * unavalible：下线
        * subscribe：订阅某用户在线状态
        * unsubscribe：取消订阅某用户在线状态
        * subscribed：授权某用户订阅
        * unsubscribed：取消授权某用户订阅
        * error：错误


    ```xml
    <presence>
        <show>away</show>
        <status>show to do something</status>
    </presence>
    ```
    
    * `<show>`可选参数：
        * chat：在线，愿意聊天
        * away：短时间不在
        * xa：长时间不在
        * dnd：不想被打扰

* ####message结构####

```xml
    <message
        from="jackson@gmail.com"
        to="jimmy@msn.com"
        type="chat">
        <body>Hello World!</body>
    </message>
```
    * `type`可选参数：
        * normal：独立消息（默认）
        * chat：一对一对话
        * groupchat：群聊（多人对话）
        * headline：头条内容
        * error：错误

* ####IQ结构(Information Query)####

```xml
    <!--request roster by get-->
    <!--from and to must be same-->
    <iq
        from="jackson@gmail.com"
        id="rr82a1z7"
        to="jackson@gmail.com"
        type="get">
        <query xmlns="jabber:iq:roster"/>
    </iq>
``` 
    * `type`可选参数：
        * get：获取数据请求，类似http的get
        * set：设置数据请求，类似http的post
        * result：响应请求
        * error：错误


    ```xml
    <!--reply request-->
    <!--id must be same to request-->
    <iq
        from="jackson@gmail.com"
        id="rr82a1z7"
        to="jackson@gmail.com"
        type="result">
        <query xmlns="jabber:iq:roster">
            <item jid="jimmy@msn.com"/>
            <item jid="tom@hotmail.com"/>
        </query>
    </iq>
    ```
    
