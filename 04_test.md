```bash
lerobot-rollout \
  --strategy.type=base \
  --policy.path=ziyiweng/act_so101_flextape_dataset_10kpolicy \
  --robot.type=so101_follower \
  --robot.port=/dev/tty.usbmodem5B140318901 \
  --robot.cameras="{ 
  front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 20},
  overhead: {type: opencv, index_or_path: 1, width: 640, height: 480, fps: 20}
}" \
  --display_data=true \
  --task="tape"
```
