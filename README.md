# GyroLock V15 — Final Candidate

GyroLock is an Android camera project with gyro XYZ based post-recording stabilization.

## Included in V15
- Prefers CameraX Full HD (FHD). If the device does not support FHD, CameraX falls back to HD or SD.
- Stabilized output is normalized to 30 FPS for smoother and more consistent playback. The camera's actual capture resolution/frame rate still depends on the device and its supported camera modes; 60 FPS is intentionally not forced because it can cause dropped frames or overheating on some phones.
- Tap any point in the preview to request autofocus and auto-exposure at that point (if supported by the camera).
- 1×, 2× and 4× zoom buttons. Actual maximum zoom depends on the device.
- Gyro trajectory smoothing strengthened for more calm framing, with more interpolation keyframes to reduce visible jumps during strong motion.
- Mirrored edge fill before the safety crop to reduce black edge gaps.
- Original recording is preserved; the stabilized copy is published to `Movies/GyroLock`.
- GitHub Actions workflow builds a debug APK artifact.

## Important stabilization limitations
The live preview transform is a visual preview only. CameraX records the camera stream, and gyro-based stabilization is applied to the saved video after recording stops. This is software stabilization, not a full Google Photos-style optical-flow/motion-vector stabilizer. Gyroscope data mainly measures rotation; strong translation from walking, parallax, rolling shutter, and motion blur cannot be perfectly removed from gyro data alone. The crop margin also limits how much correction can be applied without exposing empty edges.

## Build
1. Upload the contents of this ZIP to the root of a GitHub repository.
2. Open **Actions** and run **Build GyroLock APK** (or push to `main`/`master`).
3. Download the `GyroLock-debug-apk` artifact after the workflow succeeds.

## Validation status
The ZIP structure is checked. This environment has not built the APK or tested the app on a physical phone, so the GitHub Actions result and on-device testing are still required. First test a short clip in good light and compare the original with the stabilized output.
