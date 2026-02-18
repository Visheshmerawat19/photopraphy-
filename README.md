# photography-
wedding photos 

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CSS Project</title>
    <link rel="stylesheet" href="photo.css"/>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="photo.css">
<link href="https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&family=Roboto:ital,wght@0,100..900;1,100..900&display=swap" rel="stylesheet">   <link
  
      href="https://fonts.googleapis.com/css2?family=Poppins&display=swap"
      rel="stylesheet"
    />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"/>
  </head>
  <body>
    <div class="main_box">
      <input type="checkbox" id="check" />
      <div class="btn_one">
        <label for="check" style="color: white">
          <i class="fa-solid fa-bars"></i>
        </label>
      </div>

      <div class="sidebar_menu">
        <div class="logo">
          <a href="#">mahadev photography</a>
        </div>

        <div class="btn_two">
          <label for="check" style="color: grey">
            <i class="fa-solid fa-xmark"></i>
          </label>
        </div>

        <div class="menu">
          <ul>
            <li>
              <i class="fa-solid fa-image"></i>
              <a href="#">Gallery</a>
            </li>
            <li>
              <i class="fa-solid fa-arrow-up-right-from-square"></i>
              <a href="#">Shortcuts</a>
            </li>
            <li>
              <i class="fa-solid fa-photo-film"></i>
              <a href="#">Exhibits</a>
            </li>
            <li>
              <i class="fa-solid fa-calendar-days"></i>
              <a href="#">Events</a>
            </li>
            <li>
              <i class="fa-solid fa-store"></i>
              <a href="#">Store</a>
            </li>
            <li>
              <i class="fa-solid fa-phone"></i>
              <a href="#">Contact</a>
            </li>
            <li>
              <i class="fa-regular fa-comments"></i>
              <a href="#">Feedback</a>
            </li>
          </ul>
        </div>

        <div class="social_media">
          <ul>
            <a href="#"><i class="fa-brands fa-facebook"></i></i></a>
            <a href="#"><i class="fa-brands fa-twitter"></i></a>
            <a href="#"><i class="fa-brands fa-instagram"></i></i></a>
            <a href="#"><i class="fa-brands fa-youtube"></i></a>
          </ul>
        </div>
      </div>
    </div>
  </body>
  <script src="photo.js"></script>
</html>


css code


*{
    margin: 0;
    padding: 0;
font-family: "Inter"
}
.main_box {
    background: url("/assects/photo.jpg");
    height: 100vh;
    background-size: cover;
}
.btn_one i {
color:white;
    font-size: 30px;
    font-weight: 700;
    position:absolute ;
    left: 16px;
    line-height: 60px;
    cursor: pointer;
    transition: all 0.3s linear;


}
.sidebar_menu {
    position: fixed;
     left: -300px; 
     height: 100%;
     width: 300px;
     background-color:rgba(255, 255,255,0.1) ;
     box-shadow: 0 0 6px rgba (255,255,255,0.5);
     transition: all 0.5s linear;
}
.sidebar_menu .logo {
    position: absolute;
    width: 100px;
    line-height:20px;
    box-shadow: 0 2px 4px rgba (255,255,255,0.5);
    height: 60px;


} 
.sidebar_menu .logo a  {
    position: absolute;
    left: 50px;
    color: white;
    text-decoration: none;
    font-size:20px ;
    font-weight: 500px;
    
} 
.sidebar_menu .btn_two{
    color:gray;
    font-size: 25px;
    position:absolute ;
    left: 270px;
    line-height: 60px;
    /* opacity: 0; */
    

}


.sidebar_menu .menu{
    position: absolute;
    width: 100%;
    top: 80px;

}
.sidebar_menu .menu li{
    margin-top:6px ;
    padding: 14px 20px;
}
.sidebar_menu .menu i,a {
color: white;
text-decoration: none;
font-size: 20px;
}
.sidebar_menu.menu i{
    padding-right:8px;
}

.sidebar_menu .social_media {
    position: absolute;
    left: 25%;
    bottom: 50px;

}
.sidebar_menu .social_media i {
    color: white;
    opacity: 0.5;
    padding: 0 5px;

}
#check {
    display: none;
}
.sidebar_menu .menu li:hover {
    box-shadow: 0 0 4px rgba(255, 255,255,0.5);
}
.btn_one i :hover{
    font-size: 40px;
}
.btn_two i:hover{
    font-size: 30px;
}
.sidebar_menu .social_media i:hover {
     opacity: 1;
    transform: scale(1.1);
}
#check:checked ~ .sidebar_menu {

    left: 0;
}
#check:checked ~ .btn_one i {
    opacity: 0;
}
#check:checked ~ .sidebar_menu .btn_two i {
    opacity: 1;
}



const express = require('express');
const router = express.Router();
const multer = require('multer');
const path = require('path');
const fs = require('fs');
const Post = require('../models/Post');

const UPLOAD_DIR = process.env.UPLOAD_DIR || 'uploads';
if (!fs.existsSync(UPLOAD_DIR)) fs.mkdirSync(UPLOAD_DIR, { recursive: true });

const storage = multer.diskStorage({
  destination: (req, file, cb) => cb(null, UPLOAD_DIR),
  filename: (req, file, cb) => {
    const unique = `${Date.now()}-${Math.round(Math.random()*1e9)}`;
    const ext = path.extname(file.originalname);
    const base = file.originalname.replace(ext, '').replace(/\s+/g, '-').replace(/[^a-zA-Z0-9-_]/g, '');
    cb(null, `${base}-${unique}${ext}`);
  }
});
const upload = multer({ storage });

// Create
router.post('/', upload.single('image'), async (req, res) => {
  try {
    const { title, content, tags } = req.body;
    const tagArr = tags ? tags.split(',').map(t => t.trim()).filter(Boolean) : [];
    const image = req.file ? {
      filename: req.file.filename,
      url: `${process.env.BASE_URL || ''}/uploads/${req.file.filename}`,
      mimetype: req.file.mimetype,
      size: req.file.size
    } : null;
    const post = new Post({ title, content, tags: tagArr, image });
    await post.save();
    res.status(201).json(post);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Read list (optionally includeDeleted=true)
router.get('/', async (req, res) => {
  try {
    const includeDeleted = req.query.includeDeleted === 'true';
    const q = includeDeleted ? {} : { isDeleted: false };
    const posts = await Post.find(q).sort({ createdAt: -1 });
    res.json(posts);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Read single
router.get('/:id', async (req, res) => {
  try {
    const post = await Post.findById(req.params.id);
    if (!post) return res.status(404).json({ error: 'Not found' });
    res.json(post);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Update (with optional new image)
router.put('/:id', upload.single('image'), async (req, res) => {
  try {
    const { title, content, tags } = req.body;
    const tagArr = tags ? tags.split(',').map(t => t.trim()).filter(Boolean) : [];
    const update = { title, content, tags: tagArr, updatedAt: new Date() };
    if (req.file) {
      const image = {
        filename: req.file.filename,
        url: `${process.env.BASE_URL || ''}/uploads/${req.file.filename}`,
        mimetype: req.file.mimetype,
        size: req.file.size
      };
      // remove old file if exists
      const existing = await Post.findById(req.params.id);
      if (existing && existing.image && existing.image.filename) {
        try {
          fs.unlinkSync(path.join(UPLOAD_DIR, existing.image.filename));
        } catch (e) {}
      }
      update.image = image;
    }
    const post = await Post.findByIdAndUpdate(req.params.id, update, { new: true, runValidators: true });
    if (!post) return res.status(404).json({ error: 'Not found' });
    res.json(post);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Soft delete
router.delete('/:id', async (req, res) => {
  try {
    const post = await Post.softDelete(req.params.id);
    if (!post) return res.status(404).json({ error: 'Not found' });
    res.json({ success: true, post });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Restore
router.post('/:id/restore', async (req, res) => {
  try {
    const post = await Post.restore(req.params.id);
    if (!post) return res.status(404).json({ error: 'Not found' });
    res.json({ success: true, post });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// Permanent delete
router.delete('/:id/permanent', async (req, res) => {
  try {
    const post = await Post.findByIdAndDelete(req.params.id);
    if (!post) return res.status(404).json({ error: 'Not found' });
    if (post.image && post.image.filename) {
      try { fs.unlinkSync(path.join(UPLOAD_DIR, post.image.filename)); } catch (e) {}
    }
    res.json({ success: true });
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

module.exports = router;







