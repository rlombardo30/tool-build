# Tool Build (mechanics)

This project is a simple browser-based prototype that uses the webcam to detect motion and show a clear visual response. The goal is to help the user notice their own movement without judgment, shame, or tracking.

## 1. What data does this tool need?

This tool needs a live camera feed from the user’s local webcam. It does not need names, accounts, email addresses, audio, images saved to disk, or any personal profile data. The code only looks at the current camera frame and compares it to the previous frame in the browser’s temporary memory.

## 2. Where is the data stored?

The camera image is processed in the browser while the page is open. It is not stored in a database, a server, or a file on the device. The only place the data exists is in the current browser session in memory.

## 3. Is the data temporary or persistent?

The data is temporary. It exists only while the camera is running and while the browser tab remains open. Once the camera is stopped, the motion comparison resets and the temporary frame memory is cleared.

## 4. Does the system need memory between sessions?

No. The tool does not need memory between sessions. Each time the user presses Start Camera, the system starts from a fresh state and begins comparing frames from that moment onward.

## 5. Does the system require AI inference?

No. This tool does not use AI, machine learning, or any external model. It compares a camera frame to the previous camera frame using basic JavaScript pixel difference checks in the browser.

## 6. How many API calls are realistically required?

This tool realistically requires zero external API calls. It uses the browser’s local camera access API through `getUserMedia()`, which asks the browser for permission to use the webcam. There are no remote calls to a database, cloud service, or AI backend.

## 7. What happens if the API fails?

If the browser cannot access the camera, the user denies permission, or the camera cannot start, the tool shows a clear error state in the interface and stops the session. There is no hidden tracking, no fallback server call, and no automatic data upload.

## Input layer

The input layer includes:

- The Start Camera button
- The Stop Camera button
- The camera stream from the user’s webcam
- The video preview displayed in the page

This layer is responsible for requesting access to the camera and passing the live frames into the logic layer.

## Logic layer

The logic layer includes:

- Comparing the current frame to the previous frame
- Tracking whether motion is currently detected
- Triggering a response only when enough movement is present
- Resetting detection when the camera stops or when movement disappears

The tool keeps the comparison simple and local, using raw pixel differences rather than AI or stored history.

## Output layer

The output layer includes:

- The live camera preview
- The visible motion indicator
- The current system state text
- A clear change in the display when movement is detected

This layer is designed to make the user notice their own movement clearly and immediately.

## How the tool aligns with the Tool Intent

This tool aligns with the Tool Intent by making movement visible in real time without judging or tracking the user. It is a simple feedback system: the user sees their own body motion in the moment, and the display responds clearly while staying fully local to the browser.

## Break Log

This section is intentionally left blank for later notes, bug reports, fixes, and testing observations.

## Run locally

1. Open a terminal in this project folder.
2. Start a local web server:
   `python3 -m http.server 8000`
3. Open this URL in the browser:
   `http://localhost:8000`
4. Click Start Camera.
5. Allow webcam access when the browser asks.
6. Move in front of the camera and watch the Motion indicator change.
7. Click Stop Camera when finished.

If a camera permission dialog appears, choose Allow to continue. If permission is denied or the camera is unavailable, the tool shows an error message instead of continuing.
