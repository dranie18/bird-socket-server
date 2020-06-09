# Bird Socket Server

![Delphi Supported Versions](https://img.shields.io/badge/Delphi%20Supported%20Versions-10.1%20and%20ever-blue.svg)
![Platforms](https://img.shields.io/badge/Supported%20platforms-Win32%20and%20Win64-red.svg)

This is a websocket server for Delphi.

## Prerequisites

* `[Optional]` For ease I recommend using the Boss for installation
* [**Boss**](https://github.com/HashLoad/boss) - Dependency Manager for Delphi

## Installation using Boss (dependency manager for Delphi applications)

```html
boss install github.com/mateusvicente100/bird-socket-server
```

## Manual Installation

Add the following folder to your project, in *Project > Options > Resource Compiler > Directories and Conditionals > Include file search path*

```html
../bird-socket-server/src
```

## Getting Started

You need to use Bird.Socket

```pascal
uses Bird.Socket;
```

Create an instance of TBirdSocket and assign the methods and propertys

```pascal
procedure
var
  LServer: TBirdSocket;
begin
  LServer := TBirdSocket.Create(8080);
  try
    LServer.AddEventListener(TEventType.CONNECT,
      procedure(const AContext: TIdContext)
      begin
        // Do on connect.
      end);

    LServer.AddEventListener(TEventType.EXECUTE,
      procedure(const AContext: TIdContext)
      begin
        // Do on execute.
      end);

    LServer.AddEventListener(TEventType.DISCONNECT,
      procedure(const AContext: TIdContext)
      begin
        // Do on disconnect.
      end);
    LServer.Start;
  finally
    LServer.DisposeOf;
  end;
end;
```

## Samples

Check out our samples projects for the server and client side, with web and Delphi code. If you have any questions or suggestion, please contact, make your pull request or create an issue.

## Delphi Client

For Delphi websocket connections I recommend to use the [**bird-socket-client**](https://github.com/mateusvicente100/bird-socket-client) project. It's simple to use and install

```pascal
procedure Start;
var
  LWebSocket: TWebSocketClient;
begin
  LWebSocket := TWebSocketClient.New('ws://localhost:8080');
  LWebSocket.AddEventListener(TEventType.MESSAGE,
    procedure(const AText: string)
    begin
      Log(AText);
    end);
  LWebSocket.Connect;
  LWebSocket.Send('Hello Server');
end;
```

<p align="center">
  <img src="samples/images/sample-client-delphi.png">  
</p>  

## Web Client

For web we have native websocket connection in html

```html
<script>
  const socket = new WebSocket('ws://localhost:8080');

  socket.addEventListener('message', function (event) {
    console.log(event.data);
  });

  socket.addEventListener('open', function (event) {
    socket.send('Hello Server!');
  });
</script>  
```

<p align="center">
  <img src="samples/images/sample-client-web.png">
</p>
