# 🎬 FFmpeg Command Guide — Practical Workflow

# 📥 0. Install FFmpeg

###  On Ubuntu :
```bash
sudo apt update
sudo apt install ffmpeg
```

For Check:
```bash
ffmpeg -version
```


---

# ▶️ 1. Play or Preview Media (using `ffplay`)

-  ###   Play a video:
    ```bash
    ffplay input.mp4
    ```

- ###   Play an audio file:
    ```bash
    ffplay input.mp3
    ```

-  ###  Play without sound:
    ```bash
    ffplay -an input.mp4
    ```

-  ###  Play specific section:
    ```bash
    ffplay -ss 00:00:10 -t 00:00:05 input.mp4
    ```

---

# 🔄 2. Convert Media

- ###  Convert video format (e.g., `.mp4` → `.webm`):
    ```bash
    ffmpeg -i input.mp4 output.webm
    ```

- ###  Extract audio from video:
    ```bash
    ffmpeg -i input.mp4 output.mp3
    ```

- ###  Convert GIF → video:
    ```bash
    ffmpeg -i input.gif -movflags faststart -pix_fmt yuv420p output.mp4
    ```

---

# ✂️ 3. Cut / Trim Videos

-  ### Cut from specific time:
    ```bash
    ffmpeg -ss 00:00:05 -i input.mp4 -t 00:00:10 -c copy output.mp4
    ```

---

# 📉 4. Compress Videos

-  ### Basic compression:
    ```bash
    ffmpeg -i input.mp4 -vcodec libx264 -crf 23 output.mp4
    ```

- ###  Resize & compress:
    ```bash
    ffmpeg -i input.mp4 -vf "scale=640:-1" -vcodec libx264 -crf 23 output.mp4
    ```

---

# 🖼️ 5. Create Optimized GIFs

### ✅ Best Method (2-step palette process):

- **Step 1** – Generate palette:
    ```bash
    ffmpeg -i input.mp4 -vf "fps=10,scale=480:-1:flags=lanczos,palettegen" palette.png
    ```

- **Step 2** – Create optimized GIF:
    ```bash
    ffmpeg -i input.mp4 -i palette.png -filter_complex \
    "fps=10,scale=480:-1:flags=lanczos[x];[x][1:v]paletteuse" output.gif
    ```

 - ### 💡 Tips:  
    > - Lower `fps` and `scale` for smaller size  
    > - Example: `fps=7`, `scale=360:-1`

### 🚫 Simple Method (not recommended):
```bash
ffmpeg -i input.mp4 output.gif
```
> ⚠️ Generates large files with poor performance.

---

# 🧼 6. Audio Editing

-  ### Remove audio:
    ```bash
    ffmpeg -i input.mp4 -an output.mp4
    ```

-  ### Increase volume:
    ```bash
    ffmpeg -i input.mp4 -filter:a "volume=2.0" output.mp4
    ```

---

# ⏩ 7. Control Video Speed

- ###  Speed up (2× faster):
    ```bash
    ffmpeg -i input.mp4 -vf "setpts=0.5*PTS" -an fast.mp4
    ```

- ### Slow down (0.5× speed):
    ```bash
    ffmpeg -i input.mp4 -vf "setpts=2.0*PTS" -an slow.mp4
    ```
