```jsx
import React, { useState } from 'react';
import { Sound } from 'sound';
import { Volume } from 'plugins';
import {
  BasicControls,
  VolumeControl
} from 'player';

const Player = () => {
  const [state, setState] = useState({
    status: Sound.status.PAUSED,
    volume: 100,
    loading: false,
    position: 0
  });

  return (
    <div>
      <Sound
        url="demo.mp3"
        playStatus={state.status}
        position={state.position}
        onFinishedPlaying={() => setState({ ...state, status: Sound.status.STOPPED })}
        onLoad={() => setState({ ...state, loading: false })}
        onLoading={() => setState({ ...state, loading: true })}
        onPlaying={data => setState({ ...state, ...data  })}
      >
        <Volume value={state.volume} />
      </Sound>
      <BasicControls
        onPlay={() => setState({ ...state, status: Sound.status.PLAYING })}
        onPause={() => setState({ ...state, status: Sound.status.PAUSED })}
        onStop={() => setState({ ...state, status: Sound.status.STOPPED })}
        duration={state.duration}
        position={state.position}
        onTimeChange={evt => setState({ ...state, position: Number(evt.target.value) })}
      >
        <VolumeControl
          value={state.volume}
          onChange={evt => setState({ ...state, volume: Number(evt.target.value) })}
        />
      </BasicControls>
    </div>
  );
};

<Player />
```
