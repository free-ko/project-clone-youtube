# API를 통해 Popular Video 데이터 사용하기

<br>

app.jsx파일

```js
import React, { useEffect, useState } from "react";
import VideoList from './'
import "./app.css";

function App() {
  // videos를 담을 수 있는 변수와
  // videos의 업데이트 할수있는 함수 setVideos를 선언 합니다.
  // 초기 값은 텅텅 빈 videos 목록으로 설정 합니다.
  const [videos, setVideos] = useState([]);

  // 데이터를 받아 오거나 컴포넌트가 마운트 및 업데이트 될 때
  // useEffect를 사용 합니다.
  // 우리가 useEffect 안에 원하는 함수를 등록하면
  // 데이터를 받아 오거나 마운트 및 업데이트 될 때 등록한 함수가 호출 됩니다.
  // 그러나 컴포넌트가 업데이트 할 때마다 네트워크 통신(API를 이용해 데이터를 가져오는 것)하는 것은 좋지 않습니다.
  // 그래서 밑에 빈 배열을 2번째 인자로 전달 하면 마운트 되었을 때만 함수가 호출 됩니다.
  // 만약 배열 안에 특정 변수(videos)를 넣게 되면 그 변수가 업데이트 될 때마다 밑의 함수가 호출이 됩니다.
  useEffect(() => {
    // Postmen의 JS Fetch Code를 가져 왔습니다.
    const requestOptions = {
      method: "GET",
      redirect: "follow",
    };

    fetch(
      "https://www.googleapis.com/youtube/v3/videos?part=snippet&chart=mostPopular&maxResults=25&key=AIzaSyDr__XM5Fe4Y8yzUAqFoQFu3iUmSjYcDtE",
      requestOptions
    )
      // fetch가 정상적으로 받아지면
      // 반응을 text로 변환하고 그것을 console에 출력 하고
      // 만약 에러가 나면 console에 'error'를 표시 합니다.
      .then((response) => response.text())
      .then((result) => console.log(result))
      .catch((error) => console.log("error", error));

      // 그러나 데이터를 받아 올 때 데이터를 Text로 보는 것 보다는 Json가 보기 편합니다.
      .then((response) => response.json())
      // 받아온 데이터를 비 동기적으로 setVideos를 통해 videos에 업데이트 해줍니다.
      .then(result => setVideos(result.items))
  }, []);


// 그리고 마지막으로 받아온 데이터를 viode_list.jsx 컴포넌트에 전달해줘야 합니다.
  return <VideoList videos={videos}/>;
}

export default App;
```

<br>

video_list.jsx

```js
import React from "react";
import VideoItem from '../';

// 전달 받은 props인 videos를 map 함수를 통해 받아온 모든 video 데이터들을 VideoItem Component에 전달 합니다.
const VideoList = (props) => (
  <ul>
    {props.videos.map(video => (
      <VideoItem key={video.id} video={video}>
    ))}
  </ul>
);

export default VideoList;
```

<br>

vidoe_item.jsx

```js
import React from "react";

// 전달 받은 Props의 Title를 표현 합니다.
const VideoItem = (props) => <h1>{props.video.snippet.title}</h1>;

export default VideoItem;
```
