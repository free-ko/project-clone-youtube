# API이용

- vidoe 데이터를 가져와서 웹 화면에 표시
- 가져온 데이터를 Deconstructing을 통해 간단하게 사용 하기
- Component에 Style 적용 하기

<br>

video_item.jsx파일

```jsx
import React from "react";
import styles from './';

// 전달 받은 Props를 사용 합니다.
// props 안에서 video만 꺼내서 사용 하고 싶으면
// ({video})로 작성해서 props.video 안하고 video만 작성해서 사용 가능합니다.
// 또한 video가 아닌 다른 이름으로 사용 하고 싶다면
// ({video: videoItem}) 이런식으로 videoItem으로 사용 가능합니다.
const VideoItem = (props) => (
  <li className={styles.container}>
    <div className={styles.video}>
      <img
        className={styles.thumbnail}
        src={snippet.thumbnails.medium.url}
        alt="video thumbnail"
      />
      <div className={styles.metadata}>
        <p className={styles.title}>{snippet.title}</p>
        <p className={styles.channel}>{snippet.channelTitle}</p>
      </div>
    </div>
  </li>

  // 그런데 video.snippet도 반복적으로 사용 되는게 보입니다.
  // 이럴 때에는 ({video: { snippet }}) 으로 작성 합니다.
  // 위에처럼 작성하면 바로 snippet으로 접근이 가능합니다.
  // video.snippet --> snippet.thumbnails....
  // 이러한 것을 deconstructing이라고 합니다.
  const VideoItem = ({video}) => (
  <li>
    <img src={video.snippet.thumbnails.mdium.url} alt="video thumnail" />
    <div>
      <p>{video.snippet.title}</p>
      <p>{video.snippet.channelTitle}</p>
    </div>
  </li>
);

export default VideoItem;
```

<br>

video_item.module.css파일

```css
.container {
  width: 50%;
  padding: 0.2em;
  box-sizing: border-box;
}

.video {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  border: 1px solid lightgray;
  box-shadow: 3px 3px 5px 0px rgba(191, 191, 191, 0.53);
  cursor: pointer;
  transition: transform 250ms ease-in;
}

.video:hover {
  transform: scale(1.02);
}

.thumbnail {
  width: 40%;
  height: 100%;
}

.metadata {
  margin-left: 0.2em;
}

.title,
.channel {
  margin: 0;
  font-size: 0.8rem;
}

.channel {
  font-size: 0.6rem;
}
```

<br>

video_list.jsx파일

```jsx
import React from "react";
import VideoItem from '../';
// CSS 적용 하기
import styles from './';

const VideoList = (props) => (
  // CSS 적용하기 위해 Class Name 설정
  <ul className={styles.videos}>
    {props.videos.map(video => (
      <VideoItem key={video.id} video={video}>
    ))}
  </ul>
);

export default VideoList;
```

<br>

video_list_module.css파일

```jsx
.videos {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding-left: 0;
}
```
