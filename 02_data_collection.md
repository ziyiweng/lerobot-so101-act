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

