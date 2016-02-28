#XMPPЭ��

* ###XML Stanzas

* ####ÿ���ͻ�����JID����Ϊ��ݱ�ʶ `[user"@"]domain["/"resource]`
* ####ʾ��
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
* ####XML Stanzasͨ������
    * `from` -> ԴJID��������һ�㲻���Σ�һ���������״̬�Զ���ȡ��
    * `to` -> Ŀ��JID
    * `type` -> 
    * `id` -> �������Ϳͻ���֮��ı�ʶ��
* ####stream�ṹ
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
* ####presence�ṹ
```xml
    <presence
        from="jackson@gmail.com"
        to="jimmy@msn.com"
        type="unavailable"/>
```
    * `type`��ѡ������
        * available������
        * unavalible������
        * subscribe������ĳ�û�����״̬
        * unsubscribe��ȡ������ĳ�û�����״̬
        * subscribed����Ȩĳ�û�����
        * unsubscribed��ȡ����Ȩĳ�û�����
        * error������

    ```xml
    <presence>
        <show>away</show>
        <status>show to do something</status>
    </presence>
    ```
    * `<show>`��ѡ������
        * chat�����ߣ�Ը������
        * away����ʱ�䲻��
        * xa����ʱ�䲻��
        * dnd�����뱻����

* ####message�ṹ
```xml
    <message
        from="jackson@gmail.com"
        to="jimmy@msn.com"
        type="chat">
        <body>Hello World!</body>
    </message>
```
    * `type`��ѡ������
        * normal��������Ϣ��Ĭ�ϣ�
        * chat��һ��һ�Ի�
        * groupchat��Ⱥ�ģ����˶Ի���
        * headline��ͷ������
        * error������
* ####IQ�ṹ(Information Query)
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
    * `type`��ѡ������
        * get����ȡ������������http��get
        * set������������������http��post
        * result����Ӧ����
        * error������

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
    