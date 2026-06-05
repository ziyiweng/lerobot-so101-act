# collect data
```bash
lerobot-record \
  --robot.type=so101_follower \
  --robot.port=/dev/tty.usbmodem5B140318901 \
  --robot.id=my_follower \
  --teleop.type=so101_leader \
  --teleop.port=/dev/tty.usbmodem5B415335771 \
  --teleop.id=my_leader \
  --robot.cameras="{ 
  front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 20},
  overhead: {type: opencv, index_or_path: 1, width: 640, height: 480, fps: 20}
}" \
  --dataset.repo_id=ziyiweng/tape \
  --dataset.single_task="tape" \
  --dataset.num_episodes=100 \
  --dataset.episode_time_s=25 \
  --dataset.reset_time_s=5 \
  --dataset.push_to_hub=false
```
Resume data collection after interruption
```bash
lerobot-record \
  --robot.type=so101_follower \
  --robot.port=/dev/tty.usbmodem5B140318901 \
  --robot.id=my_follower \
  --teleop.type=so101_leader \
  --teleop.port=/dev/tty.usbmodem5B415335771 \
  --teleop.id=my_leader \
  --robot.cameras="{ 
  front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 20},
  overhead: {type: opencv, index_or_path: 1, width: 640, height: 480, fps: 20}
}" \
  --dataset.repo_id=ziyiweng/tape_20260605_123412 \
  --dataset.single_task="tape" \
  --dataset.num_episodes=50 \
  --dataset.episode_time_s=25 \
  --dataset.reset_time_s=5 \
  --dataset.push_to_hub=false \
  --dataset.root=/Users/ziyiweng/.cache/huggingface/lerobot/ziyiweng/tape_20260605_123412 \
  --resume=True
```

