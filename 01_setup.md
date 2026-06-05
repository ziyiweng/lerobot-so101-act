# camera
```bash
python - <<'EOF'
import cv2

idx = 0

cap = cv2.VideoCapture(idx)

while True:
    ret, frame = cap.read()

    if not ret:
        break

    cv2.imshow("cam", frame)

    if cv2.waitKey(1) == 27:
        break

cap.release()
cv2.destroyAllWindows()
EOF
```
use `idx=` to switch between cameras

---

# calibration
```bash
lerobot-calibrate \
  --robot.type=so101_follower \
  --robot.port=/dev/tty.usbmodem5B140318901 \
  --robot.id=my_follower

lerobot-calibrate \
  --teleop.type=so101_leader \
  --teleop.port=/dev/tty.usbmodem5B415335771 \
  --teleop.id=my_leader
```

---

# teleporation
```bash
lerobot-teleoperate \
  --robot.type=so101_follower \
  --robot.port=/dev/tty.usbmodem5B140318901 \
  --robot.id=my_follower \
  --teleop.type=so101_leader \
  --teleop.port=/dev/tty.usbmodem5B415335771 \
  --teleop.id=my_leader 
```
optional
```bash
  --display.data=True
```
 
  
