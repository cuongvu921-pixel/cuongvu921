# cuongvu921
tiktok-live-boost/
├── src/
│   ├── index.js        # kết nối live
│   ├── events.js       # xử lý chat/gift/like
│   ├── leaderboard.js
│   └── games/
├── overlay/            # HTML dùng làm Browser Source trong OBS
├── .env.example
├── package.json
└── README.md
const { WebcastPushConnection } = require('tiktok-live-connector');

const live = new WebcastPushConnection(process.env.TIKTOK_USERNAME);

live.connect()
  .then(state => console.log('Đã kết nối phòng live:', state.roomId))
  .catch(err => console.error('Lỗi kết nối:', err));

live.on('chat', d => console.log(`${d.uniqueId}: ${d.comment}`));
live.on('gift', d => console.log(`${d.uniqueId} tặng ${d.giftName} x${d.repeatCount}`));
live.on('like', d => console.log(`${d.uniqueId} thả ${d.likeCount} tim`));
live.on('follow', d => console.log(`${d.uniqueId} vừa follow!`));
