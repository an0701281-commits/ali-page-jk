<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>ALI | Gallery</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    background: #050505;
    color: #00ff66;
    font-family: monospace;
    min-height: 100vh;
}

header {
    text-align: center;
    padding: 35px 15px 20px;
}

h1 {
    font-size: 50px;
    margin: 0;
    text-shadow: 0 0 20px #00ff66;
}

.subtitle {
    margin-top: 10px;
    color: #00cc55;
}

.upload {
    text-align: center;
    margin: 20px;
}

input[type="file"] {
    display: none;
}

label {
    display: inline-block;
    padding: 14px 25px;
    border: 2px solid #00ff66;
    cursor: pointer;
    box-shadow: 0 0 15px #00ff66;
    transition: 0.3s;
}

label:hover {
    background: #00ff66;
    color: #000;
}

.gallery {
    width: 95%;
    max-width: 1000px;
    margin: 30px auto;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
}

.gallery img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border: 1px solid #00ff66;
    box-shadow: 0 0 10px #00ff66;
    cursor: pointer;
    transition: 0.3s;
}

.gallery img:hover {
    transform: scale(1.03);
}

.empty {
    text-align: center;
    color: #008833;
    margin-top: 50px;
}

#viewer {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.95);
    justify-content: center;
    align-items: center;
    z-index: 10;
}

#viewer img {
    max-width: 90%;
    max-height: 85%;
    border: 2px solid #00ff66;
    box-shadow: 0 0 30px #00ff66;
}

.close {
    position: absolute;
    top: 20px;
    right: 25px;
    font-size: 35px;
    cursor: pointer;
    color: #00ff66;
}
</style>
</head>

<body>

<header>
    <h1>ALI</h1>
    <div class="subtitle">/// PHOTO GALLERY ///</div>
</header>

<div class="upload">
    <label for="photos">＋ إضافة صور</label>
    <input id="photos" type="file" accept="image/*" multiple>
</div>

<div class="gallery" id="gallery">
    <div class="empty">لا توجد صور حاليًا</div>
</div>

<div id="viewer">
    <span class="close" onclick="closeViewer()">×</span>
    <img id="bigImage">
</div>

<script>
const input = document.getElementById("photos");
const gallery = document.getElementById("gallery");

input.addEventListener("change", function() {

    const files = Array.from(this.files);

    if (files.length > 0) {
        gallery.innerHTML = "";
    }

    files.forEach(file => {

        if (!file.type.startsWith("image/")) return;

        const img = document.createElement("img");

        img.src = URL.createObjectURL(file);

        img.onclick = function() {
            document.getElementById("bigImage").src = img.src;
            document.getElementById("viewer").style.display = "flex";
        };

        gallery.appendChild(img);
    });
});

function closeViewer() {
    document.getElementById("viewer").style.display = "none";
}
</script>

</body>
</html>
