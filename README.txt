SIH submission round 2 -- 3D model from drone video
=====================================================

input_video.mp4             The 60-second source clip (drone orbit around Toolse
                             castle ruin, Estonia)
3D_model_toolse_castle.ply  THE RESULT -- a photo-real 3D Gaussian splat. Open with
                             the Brush viewer, or in Blender via the "3DGS Render by
                             KIRI Engine" add-on (github.com/Kiri-Innovation/
                             3dgs-render-blender-addon).
proof_real_vs_rendered.jpg  4 real photos (left) vs. what the trained 3D model
                             renders from the SAME camera angle it never trained on
                             (right) -- this is how you verify the model is real 3D,
                             not just a lookup of the input photos.
CREDITS.txt                  Source video licence + software used.

How it was made
----------------
1. 36 frames sampled evenly from the 60s video.
2. VGGT worked out the camera position for every frame (~7 min).
3. Brush trained the photo-real 3D scene from those frames + camera positions
   (15,000 steps, 1024px -- 18 minutes).
Total: ~25 minutes, on a Mac, no NVIDIA GPU.

Quality check
-------------
4 frames were held back from training entirely, then rendered from the finished
model and compared pixel-by-pixel against the real photo from that same angle:
  frame 0000: 24.0 dB PSNR
  frame 0009: 27.5 dB PSNR
  frame 0018: 21.4 dB PSNR
  frame 0027: 25.2 dB PSNR
(Higher = closer match. 20+ dB with matching detail, as seen here, is a strong
result -- see proof_real_vs_rendered.jpg to judge visually.)
