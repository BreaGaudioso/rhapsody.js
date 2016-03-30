# Rhapsody.js

### Getting Started
Include the rhapsody.js source in your application after the dependent jQuery library. Once the source is loaded, the library must be initialized with an application key.

```javascript
Rhapsody.init({
  consumerKey: 'foo'
});
```

#### Initialization Options
| Attribute      | Default        | Description   |
| -------------- | -------------- | ------------- |
| consumerKey    | undefined      | The application key |
| version        | 'v1'           | API endpoint version |
| catalog        | 'EN'           | The desired catalog locale |
| player         | 'player-frame' | The html element id where the player iframe will be embedded |

### Authentication
The Member object exposes a methods for user sessions. Use the `Rhapsody.member.set(credentials)` to manage sessions. After setting the member session information the player will automatically be reauthenticated.

```javascript
Rhapsody.member.set({
  accessToken: 'oauth access token',
  refreshToken: 'oauth refresh token'
});
```

### Playback
The Rhapsody object exposes a top-level `player` object that provides the necessary methods to manage playback.

### Check if player is ready and authorize 

```javascript
Rhapsody.player.on('ready', function(e) {
    Rhapsody.member.set({accessToken: 'oauth access token'}); // If not set earlier
    Rhapsody.player.auth();
}
```

#### Playing a track
```javascript
Rhapsody.player.play('Tra.5156528');
```

#### Pausing
```javascript
Rhapsody.player.pause();
```

#### Seek
For example, to seek to 0:10 in a given track:

```javascript
Rhapsody.player.seek();
```

#### Volume

Set volume between muted (0) and max (1.0)

```javascript
Rhapsody.player.setVolume(.5);
```

### Data
The Rhapsody object exposes some API convenience methods. There are methods for HTTP GET, POST, PUT, and DELETE. The first parameter determines if a secure request is made.

```javascript
Rhapsody.api.get(false, '/tracks/top', function(tracks) {
  Rhapsody.player.play(tracks[0].id);
});
```

### Events
There are a number of interesting playback-related events you can listen for:

* playevent: Starts, pauses, completes, etc.
* playtimer: Current time, total time, waveform data
* error: Bad things
* metadata
* ready
* playsessionexpired
* playstopped

Listening for player events is simple:

```javascript
Rhapsody.player.on('playevent', function(e) {
  console.log(e.data);
});

Rhapsody.player.on('playtimer', function(e) {
  console.log(e.data);
});

Rhapsody.player.on('error', function(e) {
  console.log(e.data);
});
```
