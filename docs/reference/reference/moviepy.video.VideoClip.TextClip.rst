Pythonfrom moviepy.editor import *

# Kích thước video
WIDTH, HEIGHT = 1280, 720
DURATION_PER_IMAGE = 3

# Phần intro
title = TextClip(
    "SÔNG LAM NGHỆ AN",
    fontsize=80,
    color="yellow",
    font="Arial-Bold",
    stroke_color="black",      # Thêm viền đen cho chữ dễ đọc hơn
    stroke_width=2
).set_duration(3).set_position("center")

subtitle = TextClip(
    "Niềm tự hào xứ Nghệ",
    fontsize=40,
    color="white",
    font="Arial"
).set_duration(3).set_position(("center", HEIGHT - 150))

logo = ImageClip("slna_logo.png") \
    .resize(height=200) \
    .set_duration(3) \
    .set_position(("center", 80))

intro = CompositeVideoClip(
    [title, subtitle, logo],
    size=(WIDTH, HEIGHT),
    bg_color=(0, 100, 0)       # Màu nền xanh lá đậm
).set_duration(3)

# Slideshow ảnh
image_files = ["slna1.jpg", "slna2.jpg"]  # Thêm ảnh ở đây nếu có nhiều hơn
images = []
for img_path in image_files:
    clip = ImageClip(img_path) \
        .resize((WIDTH, HEIGHT)) \
        .set_duration(DURATION_PER_IMAGE) \
        .crossfadein(0.5) \   # Mượt hơn fadein/out riêng
        .crossfadeout(0.5)
    images.append(clip)

slideshow = concatenate_videoclips(images, method="compose")

# Nhạc nền
total_duration = intro.duration + slideshow.duration
music = AudioFileClip("music.mp3").subclip(0, total_duration).volumex(0.8)  # Giảm âm lượng chút nếu cần

# Ghép video
final_video = concatenate_videoclips([intro, slideshow])
final_video = final_video.set_audio(music)

# Xuất file
final_video.write_videofile(
    "slna_video.mp4",
    fps=24,
    codec="libx264",
    audio_codec="aac",
    threads=4,                 # Tăng tốc render nếu máy nhiều core
    preset="medium"            # Cân bằng chất lượng/tốc độ
)

# Giải phóng bộ nhớ
final_video.close()

.. custom class to enable complete documentation of every function
   see https://stackoverflow.com/a/62613202

moviepy.video.VideoClip.TextClip
================================

.. currentmodule:: moviepy.video.VideoClip

.. autoclass:: TextClip
   :members:

   
