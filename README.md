<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub MP3 플레이어</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #f4f7f6;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .player-container {
            background-color: #ffffff;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            text-align: center;
            width: 350px;
        }
        h2 {
            margin-top: 0;
            color: #333;
            font-size: 1.5rem;
        }
        .song-title {
            font-size: 1.1rem;
            color: #666;
            margin-bottom: 20px;
            font-weight: bold;
        }
        audio {
            width: 100%;
            margin-top: 10px;
        }
        .playlist {
            margin-top: 25px;
            text-align: left;
            max-height: 150px;
            overflow-y: auto;
            border-top: 1px solid #eee;
            padding-top: 15px;
        }
        .playlist-item {
            padding: 10px;
            cursor: pointer;
            border-radius: 5px;
            transition: background 0.2s;
            font-size: 0.9rem;
            color: #444;
        }
        .playlist-item:hover {
            background-color: #f0f0f0;
        }
        .playlist-item.active {
            background-color: #e0f2fe;
            color: #0366d6;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="player-container">
    <h2>My Music Player</h2>
    <div id="songTitle" class="song-title">곡을 선택해주세요</div>
    
    <audio id="audioPlayer" controls></audio>

    <div class="playlist" id="playlist">
        </div>
</div>

<script>
    // ★ 중요: 본인의 깃허브 RAW MP3 파일 주소로 대체하세요!
    const songs = [
        {
            title: "음악 파일 1",
            url: "https://raw.githubusercontent.com/유저이름/레포지토리이름/main/music1.mp3"
        },
        {
            title: "음악 파일 2",
            url: "https://raw.githubusercontent.com/유저이름/레포지토리이름/main/music2.mp3"
        },
        {
            title: "음악 파일 3",
            url: "https://raw.githubusercontent.com/유저이름/레포지토리이름/main/music3.mp3"
        }
    ];

    const audioPlayer = document.getElementById('audioPlayer');
    const songTitle = document.getElementById('songTitle');
    const playlistContainer = document.getElementById('playlist');

    // 플레이리스트 생성 함수
    function createPlaylist() {
        songs.forEach((song, index) => {
            const item = document.createElement('div');
            item.classList.add('playlist-item');
            item.innerText = `${index + 1}. ${song.title}`;
            
            // 클릭 시 해당 곡 재생
            item.addEventListener('click', () => {
                playSong(index);
            });
            
            playlistContainer.appendChild(item);
        });
    }

    // 곡 재생 함수
    function playSong(index) {
        // 기존 active 클래스 제거
        const items = document.querySelectorAll('.playlist-item');
        items.forEach(item => item.classList.remove('active'));

        // 현재 곡 활성화 및 재생
        items[index].classList.add('active');
        songTitle.innerText = songs[index].title;
        audioPlayer.src = songs[index].url;
        audioPlayer.play();
    }

    // 초기화
    createPlaylist();
    
    // 첫 번째 곡 세팅 (자동 재생은 안 됨)
    if(songs.length > 0) {
        songTitle.innerText = songs[0].title;
        audioPlayer.src = songs[0].url;
        document.querySelectorAll('.playlist-item')[0].classList.add('active');
    }
</script>

</body>
</html>
