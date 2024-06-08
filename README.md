ConnectServer API Documentation

This document provides an overview and detailed explanation of the ConnectServer API. The API facilitates the connection between clients and the server using WebSockets and provides functionalities to manage playback in a media application.

ConnectServer API Documentation

This document provides an overview and detailed explanation of the ConnectServer API. The API facilitates the connection between clients and the server using WebSockets and provides functionalities to manage playback in a media application.
Table of Contents

    Getting Started
    Dependencies
    Environment Setup
    API Endpoints
    WebSocket Events
    License

Getting Started
Overview

The ConnectServer API is designed to manage playback functionalities through WebSocket connections. It uses Dart as the programming language and leverages various Dart packages to handle server operations, WebSocket connections, and media playback controls.
Features

    WebSocket Support: Real-time communication with clients.
    Playback Controls: Control media playback (play, pause, stop, next, previous, seek, shuffle, loop, etc.).
    Service Discovery: Uses Bonjour for service discovery on the network.
    Error Handling: Comprehensive error reporting using the catcher_2 package.

Dependencies

Ensure the following Dart packages are included in your pubspec.yaml:

yaml

dependencies:
  async: ^2.8.1
  catcher_2: ^2.0.0
  shelf: ^1.2.0
  shelf_io: ^1.0.0
  flutter_riverpod: ^1.0.3
  shelf_router: ^1.1.0
  shelf_web_socket: ^0.2.4
  spotube:
    git:
      url: https://github.com/KRTirtho/spotube.git
  bonsoir: ^2.0.0
  web_socket_channel: ^2.1.0

Environment Setup

    Clone the repository:

    sh

git clone https://github.com/your-username/connect-server.git
cd connect-server

Install dependencies:

sh

dart pub get

Run the server:

sh

    dart run lib/main.dart

API Endpoints
GET /ping

    Description: Health check endpoint to ensure the server is running.
    Response: 200 OK with the body pong.

GET /ws

    Description: WebSocket endpoint for real-time communication.
    Response: Upgrades the connection to a WebSocket connection.

WebSocket Events

The WebSocket endpoint supports various events for managing playback. Below are the events and their purposes:
Events from Server to Client

    WebSocketQueueEvent
        Description: Sends the current queue of tracks.
        Format:

        json

    {
      "event": "queue",
      "data": [...]
    }

WebSocketPlayingEvent

    Description: Sends the current playing state.
    Format:

    json

    {
      "event": "playing",
      "data": true
    }

WebSocketPositionEvent

    Description: Sends the current position of the track.
    Format:

    json

    {
      "event": "position",
      "data": "00:01:30"
    }

WebSocketDurationEvent

    Description: Sends the duration of the current track.
    Format:

    json

    {
      "event": "duration",
      "data": "00:03:45"
    }

WebSocketShuffleEvent

    Description: Sends the shuffle state.
    Format:

    json

    {
      "event": "shuffle",
      "data": true
    }

WebSocketLoopEvent

    Description: Sends the loop mode.
    Format:

    json

    {
      "event": "loop",
      "data": "none"
    }

WebSocketVolumeEvent

    Description: Sends the current volume level.
    Format:

    json

    {
      "event": "volume",
      "data": 0.8
    }

WebSocketErrorEvent

    Description: Sends error messages.
    Format:

    json

        {
          "event": "error",
          "data": "Error message"
        }

Events from Client to Server

    Load Event
        Description: Loads a new queue of tracks.
        Format:

        json

    {
      "event": "load",
      "data": {
        "tracks": [...],
        "initialIndex": 0
      }
    }

Play/Pause Event

    Description: Toggles play and pause.
    Format:

    json

    {
      "event": "play_pause"
    }

Stop Event

    Description: Stops the playback.
    Format:

    json

    {
      "event": "stop"
    }

Next Event

    Description: Skips to the next track.
    Format:

    json

    {
      "event": "next"
    }

Previous Event

    Description: Returns to the previous track.
    Format:

    json

    {
      "event": "previous"
    }

Seek Event

    Description: Seeks to a specific position in the track.
    Format:

    json

    {
      "event": "seek",
      "data": "00:01:30"
    }

Shuffle Event

    Description: Toggles shuffle mode.
    Format:

    json

    {
      "event": "shuffle",
      "data": true
    }

Loop Event

    Description: Sets the loop mode.
    Format:

    json

    {
      "event": "loop",
      "data": "one"
    }

Volume Event

    Description: Sets the volume level.
    Format:

    json

{
  "event": "volume",
  "data": 0.8
}
