
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no">
  <meta property="og:title" content="BerMatMods">
  <title>BerMatMods</title>
  <meta name="referrer" content="strict-origin-when-cross-origin">
  <link rel="icon" type="image/png" href="./assets/ico_logo.png" sizes="16x16">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Sans:wght@300;400;500;700&amp;family=Noto+Sans+JP:wght@300;400;500;700&amp;family=Noto+Sans+KR:wght@300;400;500;700&amp;family=Noto+Sans+SC:wght@300;400;500;700&amp;family=Noto+Sans+TC:wght@300;400;500;700&amp;family=Noto+Sans+Arabic:wght@300;400;500;700&amp;family=Noto+Sans+Devanagari:wght@300;400;500;700&amp;family=Noto+Sans+Hebrew:wght@300;400;500;700&amp;family=Noto+Sans+Thai:wght@300;400;500;700&amp;display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
  <!-- Estilos internos -->
  <style>
    .text-white {
      color: white !important;
    }

    .btn-fullscreen-toggle {
      background-color: rgba(255, 105, 180, 0.3);
      border: 1px solid rgba(255, 105, 180, 0.5);
      border-radius: 50%;
      cursor: pointer;
      padding: 10px;
      transition: all 0.3s ease;
    }

    .btn-fullscreen-toggle:hover {
      background-color: rgba(255, 105, 180, 0.6);
      transform: scale(1.1);
      box-shadow: 0 0 15px rgba(255, 105, 180, 0.5);
    }

    body.portrait-mode #landscape-warning {
      display: flex;
      opacity: 1;
    }

    /* ---- MÀN HÌNH CẢNH BÁO XOAY NGANG ---- */
    #landscape-warning {
      position: fixed;
      z-index: 9999;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: radial-gradient(ellipse at center, #1c1a3a 0%, #0c0a1f 100%);
      color: #e0eaff;
      display: none;
      justify-content: center;
      align-items: center;
      text-align: center;
      opacity: 0;
      pointer-events: none;
      transition: opacity 0.5s ease-in-out;
    }

    body.portrait #landscape-warning {
      display: flex;
      opacity: 1;
      pointer-events: auto;
    }

    #landscape-warning .warning-content {
      position: relative;
      z-index: 2;
      padding: 2rem 2.5rem;
      border-radius: 20px;
      background: rgba(28, 26, 58, 0.6);
      backdrop-filter: blur(10px);
      border: 1.5px solid rgba(173, 216, 230, 0.3);
      box-shadow:
        0 0 40px rgba(78, 88, 216, 0.5),
        0 0 15px rgba(255, 255, 255, 0.1),
        inset 0 0 8px rgba(173, 216, 230, 0.2);
      transform: scale(0.95);
      opacity: 0;
      animation: fadeInContent 0.6s 0.2s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
    }

    @keyframes fadeInContent {
      to {
        transform: scale(1);
        opacity: 1;
      }
    }

    #landscape-warning h1 {
      font-family: 'Orbitron', 'Montserrat', sans-serif;
      font-size: 2rem;
      margin-bottom: 0.5rem;
      letter-spacing: 1.5px;
      color: #ffffff;
      text-shadow: 0 0 12px rgba(230, 230, 255, 0.8), 0 0 4px rgba(255, 255, 255, 1);
    }

    #landscape-warning h1:nth-of-type(2) {
      font-size: 1.5rem;
      margin-bottom: 1.5rem;
      opacity: 0.8;
    }

    #landscape-warning p {
      font-size: 1.1rem;
      color: #c0c8ff;
      line-height: 1.5;
      text-shadow: 0 0 6px rgba(192, 200, 255, 0.7);
    }

    #landscape-warning p:last-of-type {
      margin-top: 1rem;
      font-weight: bold;
      letter-spacing: 1px;
    }

    #landscape-warning .stars-bg {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: 1;
      pointer-events: none;
      background: transparent;
      overflow: hidden;
    }

    #landscape-warning .stars-bg::before,
    #landscape-warning .stars-bg::after {
      content: '';
      position: absolute;
      width: 200%;
      height: 200%;
      top: -50%;
      left: -50%;
      background-image:
        radial-gradient(circle, #fff 1px, transparent 1px),
        radial-gradient(circle, #c0c8ff 1px, transparent 1px),
        radial-gradient(circle, #fff 0.5px, transparent 0.5px);
      background-size: 100px 100px, 150px 150px, 60px 60px;
      background-position: 0 0, 50px 50px, 30px 30px;
      opacity: 0;
      animation: stars-move 30s linear infinite, fadeInStars 1s ease-out forwards;
    }

    #landscape-warning .stars-bg::after {
      background-size: 150px 150px, 80px 80px, 120px 120px;
      background-position: 75px 75px, 40px 40px, 10px 10px;
      animation-duration: 45s;
    }

    @keyframes fadeInStars {
      to {
        opacity: 0.6;
      }
    }

    @keyframes stars-move {
      from {
        transform: translateY(0);
      }

      to {
        transform: translateY(-50%);
      }
    }

    #romantic-title {
      position: absolute;
      left: 50%;
      transform: translate(-50%);
      color: #ffffff;
      font-size: 2.5rem;
      font-family: 'Noto Sans', cursive;
      text-align: center;
      max-width: 60%;
      line-height: 1.2;
      word-wrap: break-word;
      text-shadow: 0 0 15px #ff69b4, 0 0 5px #ffffff;
      animation: glow 2s ease-in-out infinite alternate;
      padding: 0 10px;
    }

    @keyframes glow {
      from {
        text-shadow: 0 0 10px #ff69b4, 0 0 5px #ffffff;
      }
      to {
        text-shadow: 0 0 20px #ff69b4, 0 0 10px #ffffff;
      }
    }

    @media (max-width: 600px) {
      #romantic-title {
        font-size: 1.5rem;
      }
    }

    .music-control {
      position: fixed;
      top: 20px;
      right: 20px;
      z-index: 1000;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .music-btn {
      width: 50px;
      height: 50px;
      background: linear-gradient(135deg, #ff4d6d, #e6395c);
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.4);
      transition: all 0.3s ease;
    }

    .music-btn:hover {
      transform: scale(1.1);
      box-shadow: 0 8px 20px rgba(255, 77, 109, 0.6);
    }

    .music-btn:active {
      transform: scale(0.95);
    }

    .music-btn svg {
      width: 24px;
      height: 24px;
      fill: #fff;
    }

    .volume-control {
      width: 120px;
      background: rgba(255, 255, 255, 0.15);
      padding: 10px;
      border-radius: 10px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.4);
      border: 1px solid rgba(255, 77, 109, 0.5);
      margin-top: 10px;
      display: none;
      opacity: 0;
      transform: translateY(-10px);
      transition: opacity 0.3s ease, transform 0.3s ease;
    }

    .volume-control.visible {
      display: block;
      opacity: 1;
      transform: translateY(0);
    }

    .volume-control input {
      width: 100%;
      height: 8px;
      background: rgba(255, 255, 255, 0.3);
      border-radius: 4px;
      outline: none;
      cursor: pointer;
      -webkit-appearance: none;
    }

    .volume-control input::-webkit-slider-thumb {
      -webkit-appearance: none;
      width: 16px;
      height: 16px;
      background: #ff4d6d;
      border-radius: 50%;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
    }

    .volume-control input::-moz-range-thumb {
      width: 16px;
      height: 16px;
      background: #ff4d6d;
      border-radius: 50%;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
      border: none;
    }

    /* Mobile adjustments */
    @media only screen and (max-width: 768px) {
      .music-control {
        right: 15px;
      }

      .music-btn {
        width: 35px;
        height: 35px;
      }

      .music-btn svg {
        width: 22px;
        height: 22px;
      }

      .volume-control {
        width: 100px;
        margin-top: 8px;
      }

      .volume-control input {
        height: 10px;
      }

      .volume-control input::-webkit-slider-thumb {
        width: 18px;
        height: 18px;
      }

      .volume-control input::-moz-range-thumb {
        width: 18px;
        height: 18px;
      }
    }
  </style>
</head>
<body style="overflow: hidden; position: fixed; width: 100%; height: 100%; background: radial-gradient(circle, #200020 0%, #000000 100%);">
  <h1 id="romantic-title">BerMatMods</h1>
  <button id="toggle-fullscreen" class="text-white btn-fullscreen-toggle" style="position: absolute; top: 15px; left: 15px; z-index: 999;">
    <i id="fullscreen-icon" class="text-white fa-solid fa-expand"></i>
  </button>

  <div class="music-control">
    <button class="music-btn" id="musicBtn" aria-label="Toggle music">
      <svg id="playIcon" viewBox="0 0 24 24">
        <path d="M8 5v14l11-7z"></path>
      </svg>
      <svg id="pauseIcon" viewBox="0 0 24 24" style="display: none;">
        <path d="M6 19h4V5H6zm8-14v14h4V5z"></path>
      </svg>
    </button>
    <div class="volume-control" id="volumeControl">
      <input type="range" id="volumeSlider" min="0" max="1" step="0.01" value="0.5" aria-label="Volume control">
    </div>
  </div>

  <audio id="backgroundMusic" loop preload="auto">
    <source src="https://dedicapag.com/es/PagMemoriCorazon/musica.mp3" type="audio/mpeg">
    Tu navegador no soporta el elemento de audio.
  </audio>

  <script>
    window.dataMemoryHeartLoveLoom = {"template":"birthday-v2","data":{"title":"BerMatMods ","messages":["BerMatMods BerMatMods BerMatMods BerMatMods BerMatMods "],"images":["https:\/\/dedicapag.com\/es\/PagMemoriCorazon\/uploads\/68d2c829db5e0_1756434414.png"],"heartColor":"#ff1493"}};
  </script>

  <!-- Import Map para Three.js -->
  <script type="importmap">
    {
      "imports": {
        "three": "https://cdn.jsdelivr.net/npm/three@0.157.0/build/three.module.js",
        "three/examples/jsm/": "https://cdn.jsdelivr.net/npm/three@0.157.0/examples/jsm/"
      }
    }
  </script>

  <!-- Código Three.js Integrado (script.js) -->
  <script type="module">
    import * as THREE from "three";
    import { OrbitControls } from "https://cdn.jsdelivr.net/npm/three@0.157.0/examples/jsm/controls/OrbitControls.js";
    import { EffectComposer } from "https://cdn.jsdelivr.net/npm/three@0.157.0/examples/jsm/postprocessing/EffectComposer.js";
    import { RenderPass } from "https://cdn.jsdelivr.net/npm/three@0.157.0/examples/jsm/postprocessing/RenderPass.js";
    import { AfterimagePass } from "https://cdn.jsdelivr.net/npm/three@0.157.0/examples/jsm/postprocessing/AfterimagePass.js";

    // Función auxiliar `makeMat` (asumida, ya que no se proporcionó materials.min.js)
    function makeMat(options = {}) {
      const material = new THREE.PointsMaterial({
        map: options.map || null,
        blending: options.blending || THREE.NormalBlending,
        depthWrite: options.depthWrite !== undefined ? options.depthWrite : true,
        transparent: options.alphaSupport || false,
        vertexColors: options.vertexColors || false,
        size: options.size || 1,
        sizeAttenuation: options.sizeAttenuation !== undefined ? options.sizeAttenuation : true,
        opacity: options.opacity !== undefined ? options.opacity : 1.0
      });
      return material;
    }

    const appData = window.dataMemoryHeartLoveLoom?.data || {};
    let allWordsFlat = [];
    const originalTexts = appData.messages || [];
    originalTexts.forEach(sentence => {
      const words = sentence.split(' ');
      allWordsFlat.push(...words);
    });
    let currentWordIndex = 0;
    let nextWordSpawnTime = 0;
    const WORD_SPAWN_INTERVAL = 0.4;
    const IMAGE_CONFIG = {
      paths: appData.images || [],
      count: appData.images?.length || 0,
      scale: 2.5,
      brightnessIntensity: .4,
      spawnRate: .18,
      maxActiveImages: 45,
      spawnInterval: 400
    };
    console.log("Configuración de imagen:", IMAGE_CONFIG);
    const useCustomColor = appData.heartColor && /^#([A-Fa-f0-9]{8}|[A-Fa-f0-9]{6})$/.test(appData.heartColor);
    const heartInitialColor = new THREE.Color(useCustomColor ? appData.heartColor : '#FF69B4');
    let imageTextures = [],
      imageLoadingComplete = false,
      imagePool = [],
      activeImages = new Map(),
      freeImageIndices = [],
      currentImageIndex = 0,
      lastImageSpawnTime = 0,
      imageSpawnQueue = [],
      minActiveImages = 8,
      maxConcurrentImages = 24,
      lastStatusLogTime = 0,
      independentImageSprites = [],
      nextIndependentSpawnTime = 0;
    const textureLoader = new THREE.TextureLoader();

    async function fetchAndPrepareImageTextures() {
      try {
        const promises = IMAGE_CONFIG.paths.map(path => new Promise((resolve, reject) => {
          textureLoader.load(path, texture => {
            texture.minFilter = THREE.LinearFilter;
            texture.magFilter = THREE.LinearFilter;
            texture.format = THREE.RGBAFormat;
            texture.needsUpdate = true;
            resolve(texture);
          }, undefined, () => {
            const canvas = document.createElement("canvas");
            canvas.width = canvas.height = 512;
            const ctx = canvas.getContext("2d");
            const gradient = ctx.createRadialGradient(256, 256, 0, 256, 256, 256);
            gradient.addColorStop(0, "#ff69b4");
            gradient.addColorStop(1, "#ff1493");
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, 512, 512);
            const fallbackTexture = new THREE.CanvasTexture(canvas);
            fallbackTexture.needsUpdate = true;
            resolve(fallbackTexture);
          });
        }));
        imageTextures = await Promise.all(promises);
        return true;
      } catch (error) {
        return false;
      }
    }

    function buildImageSpriteMaterial(texture, opacity = 1) {
      return new THREE.SpriteMaterial({
        map: texture,
        transparent: true,
        opacity: opacity,
        depthWrite: false,
        alphaTest: .1,
        sizeAttenuation: true
      });
    }

    function getAspectRatioAdjustedScale(texture, scale = 2.5) {
      if (!texture || !texture.image) return scale;
      const aspect = texture.image.width / texture.image.height;
      return {
        x: aspect > 1 ? scale : scale * aspect,
        y: aspect > 1 ? scale / aspect : scale
      };
    }

    async function setupImageStreaming() {
      imageLoadingComplete = await fetchAndPrepareImageTextures();
      if (imageLoadingComplete) tweakSpawnParametersByImageCount();
    }

    function tweakSpawnParametersByImageCount() {
      const t = IMAGE_CONFIG.count;
      if (t <= 2) {
        IMAGE_CONFIG.spawnInterval = 300;
        minActiveImages = 6;
        maxConcurrentImages = Math.min(15, 7.5 * t);
      } else if (t <= 5) {
        IMAGE_CONFIG.spawnInterval = 400;
        minActiveImages = 8;
        maxConcurrentImages = Math.min(18, 3.5 * t);
      } else {
        IMAGE_CONFIG.spawnInterval = 500;
        minActiveImages = 8;
        maxConcurrentImages = Math.min(30, Math.ceil(2.5 * t));
      }
    }

    function printImageSystemReport() {
      // console.log(`Activas: ${activeImages.size}, Independientes: ${independentImageSprites.length}, Libres: ${freeImageIndices.length}, En cola: ${imageSpawnQueue.length}`);
    }

    function setupImageObjectPool() {
      if (!imageLoadingComplete || !streamHeart) return;
      imagePool.forEach(sprite => {
        if (sprite && sprite.parent) sprite.parent.remove(sprite);
      });
      imagePool.length = 0;
      activeImages.clear();
      freeImageIndices.length = 0;

      for (let i = 0; i < IMAGE_CONFIG.maxActiveImages; i++) {
        const textureIndex = i % IMAGE_CONFIG.count;
        const texture = imageTextures[textureIndex];
        const material = buildImageSpriteMaterial(texture, 1);
        const sprite = new THREE.Sprite(material);
        const aspectScale = getAspectRatioAdjustedScale(texture, IMAGE_CONFIG.scale);
        sprite.scale.set(aspectScale.x, aspectScale.y, 1);
        sprite.visible = false;
        sprite.userData = {
          poolIndex: i,
          textureIndex: textureIndex,
          isActive: false,
          particleIndex: -1,
          aspectScale: aspectScale
        };
        streamHeart.add(sprite);
        imagePool.push(sprite);
        freeImageIndices.push(i);
      }
    }

    function retrieveImageFromPool(particleIndex) {
      if (freeImageIndices.length === 0) return null;
      const poolIndex = freeImageIndices.pop();
      const sprite = imagePool[poolIndex];
      const textureIndex = currentImageIndex % IMAGE_CONFIG.count;
      const texture = imageTextures[textureIndex];
      sprite.material.map = texture;
      sprite.material.needsUpdate = true;
      const aspectScale = getAspectRatioAdjustedScale(texture, IMAGE_CONFIG.scale);
      sprite.scale.set(aspectScale.x, aspectScale.y, 1);
      sprite.userData.aspectScale = aspectScale;
      sprite.userData.textureIndex = textureIndex;
      sprite.userData.isActive = true;
      sprite.userData.particleIndex = particleIndex;
      activeImages.set(particleIndex, poolIndex);
      currentImageIndex = (currentImageIndex + 1) % IMAGE_CONFIG.count;
      return sprite;
    }

    function releaseImageToPool(particleIndex) {
      const poolIndex = activeImages.get(particleIndex);
      if (poolIndex !== undefined) {
        const sprite = imagePool[poolIndex];
        sprite.visible = false;
        sprite.material.opacity = 0;
        sprite.userData.isActive = false;
        sprite.userData.particleIndex = -1;
        activeImages.delete(particleIndex);
        freeImageIndices.push(poolIndex);
      }
    }

    function controlImageSpawningLogic(currentTime) {
      const activeCount = activeImages.size + independentImageSprites.length;
      const needsMore = activeCount < minActiveImages;
      const canSpawn = currentTime - lastImageSpawnTime >= IMAGE_CONFIG.spawnInterval && activeCount < maxConcurrentImages;

      if (!needsMore && !canSpawn) return;

      if (needsMore || currentTime >= nextIndependentSpawnTime) {
        createFloatingImageSprite(currentTime);
      }

      const bestParticleIndex = selectBestParticleForImageSpawn();
      if (bestParticleIndex !== -1 && freeImageIndices.length > 0) {
        imageSpawnQueue.push({
          particleIndex: bestParticleIndex,
          imageIndex: currentImageIndex % IMAGE_CONFIG.count,
          spawnTime: currentTime,
          isForced: needsMore
        });
        currentImageIndex = (currentImageIndex + 1) % IMAGE_CONFIG.count;
        lastImageSpawnTime = currentTime;
      }
    }

    function createFloatingImageSprite(currentTime) {
      const maxIndependent = Math.ceil(0.8 * maxConcurrentImages);
      if (independentImageSprites.length >= maxIndependent) return;

      const textureIndex = currentImageIndex % IMAGE_CONFIG.count;
      const texture = imageTextures[textureIndex];
      const material = buildImageSpriteMaterial(texture, 1);
      const sprite = new THREE.Sprite(material);
      const aspectScale = getAspectRatioAdjustedScale(texture, IMAGE_CONFIG.scale);
      sprite.scale.set(aspectScale.x, aspectScale.y, 1);
      sprite.visible = false;
      sprite.userData = {
        isIndependent: true,
        imageIndex: textureIndex,
        spawnTime: currentTime,
        lifetime: 6000 + 2000 * Math.random(),
        startY: planeYCenter,
        startX: 0,
        startZ: 0,
        aspectScale: aspectScale
      };
      streamHeart.add(sprite);
      independentImageSprites.push(sprite);
      currentImageIndex = (currentImageIndex + 1) % IMAGE_CONFIG.count;
      lastImageSpawnTime = currentTime;
      nextIndependentSpawnTime = currentTime + 1.2 * IMAGE_CONFIG.spawnInterval;
    }

    function animateFloatingImageSprites(currentTime) {
      for (let i = independentImageSprites.length - 1; i >= 0; i--) {
        const sprite = independentImageSprites[i];
        const userData = sprite.userData;
        const lifeProgress = (currentTime - userData.spawnTime) / userData.lifetime;

        if (lifeProgress >= 1) {
          streamHeart.remove(sprite);
          independentImageSprites.splice(i, 1);
          continue;
        }

        sprite.visible = true;
        const easeIn = 1 - Math.pow(1 - lifeProgress, 2);
        const targetX = 0;
        const targetY = planeYCenter;
        const targetZ = 0;
        const orbitRadius = 10 + 4 * Math.sin(lifeProgress * Math.PI * 2);
        const orbitSpeed = 1.5 + userData.imageIndex % 5 * 0.3;
        const orbitDirection = userData.imageIndex % 2 === 0 ? 1 : -1;
        const orbitAngle = lifeProgress * orbitSpeed * Math.PI * 2 * orbitDirection;
        const orbitOffset = (1 - lifeProgress) * (6 + 3 * Math.sin(userData.imageIndex));
        const easedY = THREE.MathUtils.lerp(targetY, orbitRadius, easeIn);
        const easedX = THREE.MathUtils.lerp(targetX, 0, lifeProgress);
        const easedZ = THREE.MathUtils.lerp(targetZ, 0, lifeProgress);
        const finalX = easedX + Math.cos(orbitAngle) * orbitOffset;
        const finalZ = easedZ + Math.sin(orbitAngle) * orbitOffset;

        sprite.position.set(finalX, easedY, finalZ);

        if (lifeProgress < 0.1) {
          sprite.material.opacity = lifeProgress / 0.1;
          const scale = userData.aspectScale || { x: IMAGE_CONFIG.scale, y: IMAGE_CONFIG.scale };
          sprite.scale.set(scale.x * (0.5 + 5 * lifeProgress), scale.y * (0.5 + 5 * lifeProgress), 1);
        } else if (lifeProgress > 0.4) {
          const fadeOutProgress = (lifeProgress - 0.4) / 0.6;
          sprite.material.opacity = 1 - fadeOutProgress;
          const scaleMultiplier = 1 - 0.9 * fadeOutProgress;
          const scale = userData.aspectScale || { x: IMAGE_CONFIG.scale, y: IMAGE_CONFIG.scale };
          sprite.scale.set(scale.x * scaleMultiplier, scale.y * scaleMultiplier, 1);
          if (fadeOutProgress > 0.9) sprite.visible = false;
        } else {
          sprite.material.opacity = 1;
          const scale = userData.aspectScale || { x: IMAGE_CONFIG.scale, y: IMAGE_CONFIG.scale };
          sprite.scale.set(scale.x, scale.y, 1);
        }
      }
    }

    function selectBestParticleForImageSpawn() {
      const candidates = [];
      for (let i = 0; i < streamCount; i++) {
        if (!activeImages.has(i)) {
          const state = streamState[i];
          candidates.push({
            index: i,
            state: state,
            priority: state === STATE_ASCEND ? 3 : state === STATE_ON_DISK ? 2 : 1
          });
        }
      }
      if (candidates.length === 0) return -1;
      candidates.sort((a, b) => b.priority - a.priority);
      return candidates[0].index;
    }

    function handleQueuedImageSpawns() {
      while (imageSpawnQueue.length > 0) {
        const spawnData = imageSpawnQueue.shift();
        const { particleIndex } = spawnData;
        if (!activeImages.has(particleIndex) && freeImageIndices.length > 0) {
          retrieveImageFromPool(particleIndex);
        }
      }
    }

    function applyMobileSpecificSettings() {
      if (!document.querySelector('meta[name="viewport"]')) {
        const meta = document.createElement("meta");
        meta.name = "viewport";
        meta.content = "width=device-width, initial-scale=1.0, user-scalable=no";
        document.head.appendChild(meta);
      }
      document.body.style.overflow = "hidden";
      document.body.style.position = "fixed";
      document.body.style.width = "100%";
      document.body.style.height = "100%";
      if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)) {
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      }
    }

    setupImageStreaming();

    let STAR_COUNT = 0,
      starAlpha = null,
      starPhase = null,
      starGeo = null;
    const RingText = [...appData.messages];
    let cameraAnimationStart = null;
    const CAMERA_ANIMATION_DURATION = 2.5;
    let CAMERA_START_POSITION = {
      x: 0,
      y: 90,
      z: 30
    };
    const CAMERA_END_POSITION = {
      x: 0,
      y: 25,
      z: 65
    };
    let userHasMovedCamera = false,
      streamHeartStarted = false,
      streamHeartActiveRatio = 0,
      firstResetCompleted = false;
    const scene = new THREE.Scene(),
      heartScene = new THREE.Scene(),
      renderer = new THREE.WebGLRenderer({
        antialias: true,
        alpha: true
      }),
      SPIN_HEART = false;
    let heartbeatEnabled = false;
    const fadeObjects = [];
    const explosionEffects = [];
    const effectPool = {
      waves: [],
      sparkles: [],
      texts: []
    };
    const POOL_SIZE = 5;
    const activeTexts = new Map();
    let isPulsing = false;
    let pulseStartTime = 0;
    const PULSE_DURATION = 0.6;
    const PULSE_AMPLITUDE = 0.15;
    let revealStart = null;
    const REVEAL_DURATION = 1.5,
      HEARTBEAT_FREQ_HZ = .5,
      HEARTBEAT_AMPLITUDE = .05,
      STAGE = {
        RING: 0,
        STREAM: 1,
        STAR: 2,
        SHOOT: 3,
        HEART: 4
      },
      STAGE_DURATION = .15;

    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);
    applyMobileSpecificSettings();

    let staticBottomHeart = null,
      staticTopHeart = null;
    const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, .1, 300);
    camera.position.set(0, 90, 25);
    camera.lookAt(0, 0, 0);
    const controls = new OrbitControls(camera, renderer.domElement);
    controls.enableDamping = true;
    controls.minDistance = 5;
    controls.maxDistance = 100;
    controls.enableZoom = true;
    controls.minPolarAngle = THREE.MathUtils.degToRad(60);
    controls.maxPolarAngle = THREE.MathUtils.degToRad(135);
    controls.enablePan = true;

    // PLANO INVISIBLE PARA DETECTAR CLICKS
    const planeGeo1 = new THREE.PlaneGeometry(30, 30);
    const planeMat = new THREE.MeshBasicMaterial({
      color: 0xff00ff,
      side: THREE.DoubleSide,
      visible: false
    });
    const invisiblePlane = new THREE.Mesh(planeGeo1, planeMat);
    invisiblePlane.rotation.z = Math.PI;
    invisiblePlane.position.y = 10;
    scene.add(invisiblePlane);

    const composerMain = new EffectComposer(renderer),
      renderPassMain = new RenderPass(scene, camera);
    renderPassMain.clear = false;
    composerMain.addPass(renderPassMain);
    const composerHeart = new EffectComposer(renderer);
    composerHeart.addPass(new RenderPass(heartScene, camera));
    const afterimagePass = new AfterimagePass();
    afterimagePass.uniforms.damp.value = .9;
    composerHeart.addPass(afterimagePass);
    scene.add(new THREE.AmbientLight(0xffffff, .6));
    const p1 = new THREE.PointLight(0xffffff, 1.2);
    p1.position.set(10, 10, 10);
    scene.add(p1);
    const p2 = new THREE.PointLight(0xffbfff, .8);

    function generateGlowCircleTexture() {
      const canvas = document.createElement("canvas");
      canvas.width = 256;
      canvas.height = 256;
      const ctx = canvas.getContext("2d");
      const centerX = 128,
        centerY = 128;
      const gradient1 = ctx.createRadialGradient(centerX, centerY, .4 * 127, centerX, centerY, 127);
      gradient1.addColorStop(0, "rgba(255,105,180,0.6)");
      gradient1.addColorStop(1, "rgba(255,20,147,0)");
      ctx.fillStyle = gradient1;
      ctx.beginPath();
      ctx.arc(centerX, centerY, 127, 0, 2 * Math.PI);
      ctx.closePath();
      ctx.fill();
      const gradient2 = ctx.createRadialGradient(centerX, centerY, 0, centerX, centerY, 76.2);
      gradient2.addColorStop(0, "rgba(255,255,255,1)");
      gradient2.addColorStop(1, "rgba(255,255,255,0)");
      ctx.fillStyle = gradient2;
      ctx.beginPath();
      ctx.arc(centerX, centerY, 76.2, 0, 2 * Math.PI);
      ctx.closePath();
      ctx.fill();
      const texture = new THREE.CanvasTexture(canvas);
      texture.minFilter = THREE.LinearFilter;
      texture.magFilter = THREE.LinearFilter;
      texture.needsUpdate = true;
      return texture;
    }

    p2.position.set(-10, -10, -10);
    scene.add(p2);
    const circleTexture = generateGlowCircleTexture();
    const heartShape = new THREE.Shape();
    heartShape.moveTo(5, 5);
    heartShape.bezierCurveTo(5, 5, 4, 0, 0, 0);
    heartShape.bezierCurveTo(-6, 0, -6, 7, -6, 7);
    heartShape.bezierCurveTo(-6, 11, -3, 15.4, 5, 19);
    heartShape.bezierCurveTo(12, 15.4, 16, 11, 16, 7);
    heartShape.bezierCurveTo(16, 7, 16, 0, 10, 0);
    heartShape.bezierCurveTo(7, 0, 5, 5, 5, 5);
    const polyPts = heartShape.getPoints(100);

    function isPointInsidePolygon(point, polygon) {
      let inside = false;
      for (let i = 0, j = polygon.length - 1; i < polygon.length; j = i++) {
        const xi = polygon[i].x, yi = polygon[i].y;
        const xj = polygon[j].x, yj = polygon[j].y;
        const intersect = ((yi > point.y) != (yj > point.y)) && (point.x < (xj - xi) * (point.y - yi) / (yj - yi) + xi);
        if (intersect) inside = !inside;
      }
      return inside;
    }

    const polyShift = polyPts.map(pt => ({
      x: pt.x - 5,
      y: pt.y - 7
    }));
    const BORDER_THRESHOLD = .1 * (Math.max(...polyPts.map(pt => pt.x)) - Math.min(...polyPts.map(pt => pt.x)));

    function calculateMinDistanceToBorder(x, y) {
      let minDist = Infinity;
      for (let i = 0; i < polyShift.length; i++) {
        const p1 = polyShift[i];
        const p2 = polyShift[(i + 1) % polyShift.length];
        const dx = p2.x - p1.x;
        const dy = p2.y - p1.y;
        const lenSq = dx * dx + dy * dy;
        const t = lenSq === 0 ? 0 : Math.max(0, Math.min(1, ((x - p1.x) * dx + (y - p1.y) * dy) / lenSq));
        const projX = p1.x + t * dx;
        const projY = p1.y + t * dy;
        const distSq = (x - projX) * (x - projX) + (y - projY) * (y - projY);
        if (distSq < minDist) minDist = distSq;
      }
      return Math.sqrt(minDist);
    }

    const raycaster = new THREE.Raycaster();
    const mouse = new THREE.Vector2();
    const HEART_CENTER_TARGET = new THREE.Vector3(0, 10, 0);

    function createHeartExplosion(event) {
      mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
      mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;
      raycaster.setFromCamera(mouse, camera);
      const explosionDistance = 60;
      const intersectionPoint = new THREE.Vector3();
      raycaster.ray.at(explosionDistance, intersectionPoint);

      const explosionGroup = new THREE.Group();
      const explosionMat = makeMat({
        map: circleTexture,
        blending: THREE.AdditiveBlending,
        depthWrite: false,
        alphaSupport: true,
        vertexColors: true
      });

      const count = 30 + Math.random() * 20;
      const positions = [];
      const colors = [];
      const sizes = [];
      const velocities = [];
      const baseColor = new THREE.Color().setHSL(Math.random(), 0.9, 0.7);

      for (let i = 0; i < count; i++) {
        positions.push(intersectionPoint.x, intersectionPoint.y, intersectionPoint.z);
        const color = baseColor.clone().offsetHSL(Math.random() * 0.2 - 0.1, 0, 0);
        colors.push(color.r, color.g, color.b);
        sizes.push(Math.random() * 0.8 + 0.2);
        const phi = Math.random() * Math.PI * 2;
        const theta = Math.acos(Math.random() * 2 - 1);
        const speed = Math.random() * 15 + 10;
        const velocity = new THREE.Vector3();
        velocity.setFromSphericalCoords(1, phi, theta);
        velocities.push(velocity.multiplyScalar(speed));
      }

      const geo = new THREE.BufferGeometry();
      geo.setAttribute('position', new THREE.Float32BufferAttribute(positions, 3));
      geo.setAttribute('color', new THREE.Float32BufferAttribute(colors, 3));
      geo.setAttribute('size', new THREE.Float32BufferAttribute(sizes, 1));
      const points = new THREE.Points(geo, explosionMat);
      explosionGroup.add(points);
      explosionGroup.userData.velocities = velocities;
      explosionGroup.userData.life = 1.0;
      scene.add(explosionGroup);
      explosionEffects.push(explosionGroup);
    }

    function setupEffectPools() {
      const canvas = document.createElement('canvas');
      canvas.width = 256; canvas.height = 256;
      const ctx = canvas.getContext('2d');
      const gradient = ctx.createRadialGradient(128, 128, 0, 128, 128, 128);
      gradient.addColorStop(0, 'rgba(255,255,255,1)');
      gradient.addColorStop(0.3, 'rgba(255,255,255,0.5)');
      gradient.addColorStop(1, 'rgba(255,255,255,0)');
      ctx.fillStyle = gradient;
      ctx.fillRect(0, 0, 256, 256);
      const waveTexture = new THREE.CanvasTexture(canvas);

      for (let i = 0; i < POOL_SIZE; i++) {
        const waveMat = new THREE.MeshBasicMaterial({
          map: waveTexture,
          blending: THREE.AdditiveBlending,
          transparent: true,
          depthWrite: false
        });
        const wave = new THREE.Mesh(new THREE.PlaneGeometry(20, 20), waveMat);
        wave.visible = false;
        wave.userData.active = false;
        scene.add(wave);
        effectPool.waves.push(wave);

        const SPARKLE_COUNT = 100;
        const sparkleGeo = new THREE.BufferGeometry();
        sparkleGeo.setAttribute('position', new THREE.BufferAttribute(new Float32Array(SPARKLE_COUNT * 3), 3).setUsage(THREE.DynamicDrawUsage));
        const sparkleMat = makeMat({ map: circleTexture, blending: THREE.AdditiveBlending, alphaSupport: true, depthWrite: false });
        const sparkles = new THREE.Points(sparkleGeo, sparkleMat);
        sparkles.visible = false;
        sparkles.userData.active = false;
        scene.add(sparkles);
        effectPool.sparkles.push(sparkles);
      }

      const uniqueWords = [...new Set(allWordsFlat.filter(word => word.length > 0))];
      uniqueWords.forEach(word => {
        const textTexture = createFlyingTextTexture(word);
        const textMat = new THREE.SpriteMaterial({
          map: textTexture,
          transparent: true,
          depthWrite: false,
          blending: THREE.AdditiveBlending
        });
        const textSprite = new THREE.Sprite(textMat);
        const aspectRatio = textTexture.image.width / textTexture.image.height;
        textSprite.scale.set(aspectRatio * 1.5, 1.5, 1);
        textSprite.visible = false;
        textSprite.userData.active = false;
        textSprite.userData.text = word;
        streamHeart.add(textSprite);
        effectPool.texts.push(textSprite);
      });
    }

    function releaseTextToPool(particleIndex) {
      if (activeTexts.has(particleIndex)) {
        const sprite = activeTexts.get(particleIndex);
        sprite.visible = false;
        sprite.userData.active = false;
        activeTexts.delete(particleIndex);
      }
    }

    function createFlyingTextTexture(text) {
      const canvas = document.createElement("canvas");
      canvas.width = 1024;
      canvas.height = 128;
      const ctx = canvas.getContext("2d");
      ctx.font = 'bold 70px "Noto Sans", "Noto Sans JP", "Noto Sans KR", "Noto Sans SC", "Noto Sans TC", "Noto Sans Arabic", "Noto Sans Devanagari", "Noto Sans Hebrew", "Noto Sans Thai", sans-serif';
      ctx.textAlign = "center";
      ctx.textBaseline = "middle";
      ctx.strokeStyle = "rgba(160, 30, 95, 0.9)";
      ctx.lineWidth = 8;
      ctx.strokeText(text, canvas.width / 2, canvas.height / 2);
      ctx.fillStyle = "#ffffff";
      ctx.fillText(text, canvas.width / 2, canvas.height / 2);
      const texture = new THREE.CanvasTexture(canvas);
      texture.minFilter = THREE.LinearFilter;
      texture.magFilter = THREE.LinearFilter;
      return texture;
    }

    const positions = [],
      sampleCount = 7000,
      xs = polyPts.map(pt => pt.x),
      ys = polyPts.map(pt => pt.y),
      minX = Math.min(...xs),
      maxX = Math.max(...xs),
      minY = Math.min(...ys),
      maxY = Math.max(...ys),
      threshold = minY + (maxY - minY) / 6;

    while (positions.length / 3 < 7000) {
      const x = Math.random() * (maxX - minX) + minX;
      const y = Math.random() * (maxY - minY) + minY;
      if (isPointInsidePolygon({ x: x, y: y }, polyPts)) {
        let minDistSq = Infinity;
        for (let i = 0; i < polyPts.length; i++) {
          const p1 = polyPts[i];
          const p2 = polyPts[(i + 1) % polyPts.length];
          const dx = p2.x - p1.x;
          const dy = p2.y - p1.y;
          const lenSq = dx * dx + dy * dy;
          const t = lenSq === 0 ? 0 : Math.max(0, Math.min(1, ((x - p1.x) * dx + (y - p1.y) * dy) / lenSq));
          const projX = p1.x + t * dx;
          const projY = p1.y + t * dy;
          const distSq = (x - projX) * (x - projX) + (y - projY) * (y - projY);
          if (distSq < minDistSq) minDistSq = distSq;
        }
        const density = 1 / (1 + 2 * Math.sqrt(minDistSq));
        if (Math.random() < density) {
          const z = 3.6 * (Math.random() - .5);
          positions.push(x - 5, y - 7, z);
        }
      }
    }

    let minZ = Infinity,
      maxZval = -Infinity;
    for (let i = 2; i < positions.length; i += 3) {
      const z = positions[i];
      if (z < minZ) minZ = z;
      if (z > maxZval) maxZval = z;
    }

    const heartDepth = maxZval - minZ,
      heartWidth = maxX - minX,
      planeXVar = 2 * heartWidth,
      rStreamStart = .8 * heartWidth,
      Rmax = rStreamStart,
      rVortex = .6 * heartWidth,
      planeZVar = 15 * heartDepth,
      planeYCenter = maxY,
      planeYVar = 1,
      riseDuration = 10,
      fallDuration = 0,
      holdDuration = 0,
      MIN_STREAM_RISE = 8,
      MAX_STREAM_RISE = 12,
      INDENT_Y = maxY - .25 * (maxY - minY),
      INDENT_HALF_WIDTH = .35 * heartWidth,
      COS_ANGLE_THRESH = .707106,
      CLIP_FRONT_Z = .3,
      staticGeo = new THREE.BufferGeometry(),
      originalPositions = positions.slice();

    staticGeo.setAttribute("position", new THREE.Float32BufferAttribute(originalPositions, 3));

    const colors = [];
    for (let i = 0; i < positions.length; i += 3) {
      colors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
    }
    staticGeo.setAttribute("color", new THREE.Float32BufferAttribute(colors, 3));

    const staticSizes = new Float32Array(positions.length / 3),
      SIZE_SCALE = 2;
    for (let i = 0; i < staticSizes.length; i++) {
      staticSizes[i] = 2 * (.3 * Math.random() + .2);
    }
    staticGeo.setAttribute("size", new THREE.Float32BufferAttribute(staticSizes, 1));

    const topIndices = [];
    for (let i = 0; i < positions.length; i += 3) {
      if (positions[i + 1] > threshold + .1 * (Math.random() - .5) * (maxY - minY)) {
        topIndices.push(i / 3);
      }
    }
    const topSet = new Set(topIndices);

    let bottomPositions = [];
    const bottomColors = [],
      bottomSizes = [],
      bottomSizesBase = [],
      topPositionsArr = [],
      topColors = [],
      topSizes = [],
      topAlpha = [],
      idxToTopIdx = new Int32Array(positions.length / 3).fill(-1);

    for (let i = 0, topIdx = 0; i < positions.length; i += 3) {
      const idx = i / 3;
      const size = staticSizes[idx];
      const x = positions[i];
      const y = positions[i + 1];
      const z = positions[i + 2];
      if (topSet.has(idx)) {
        topPositionsArr.push(x, y, z);
        topColors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
        topSizes.push(size);
        const isIndent = Math.abs(x) < INDENT_HALF_WIDTH && y > INDENT_Y;
        topAlpha.push(isIndent ? 0 : 1);
        idxToTopIdx[idx] = topIdx++;
      } else {
        bottomPositions.push(x, y, z);
        bottomColors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
        bottomSizes.push(size);
      }
    }

    staticGeo.setAttribute("position", new THREE.Float32BufferAttribute(topPositionsArr, 3));
    staticGeo.setAttribute("color", new THREE.Float32BufferAttribute(topColors, 3));
    staticGeo.setAttribute("size", new THREE.Float32BufferAttribute(topSizes, 1));
    staticGeo.setAttribute("alpha", new THREE.BufferAttribute(new Float32Array(topAlpha), 1));
    staticGeo.attributes.position.needsUpdate = true;
    staticGeo.attributes.alpha.needsUpdate = true;

    const topCount = topPositionsArr.length / 3,
      topRadiusArr = new Float32Array(topCount),
      topPhaseArr = new Float32Array(topCount),
      topDelayArr = new Float32Array(topCount);

    for (let i = 0; i < topCount; i++) {
      const x = topPositionsArr[3 * i];
      const z = topPositionsArr[3 * i + 2];
      const radius = Math.sqrt(x * x + z * z);
      topRadiusArr[i] = radius;
      topPhaseArr[i] = Math.atan2(z, x);
      topDelayArr[i] = 10 * Math.random();
    }

    const GLOBAL_SPIRAL_FREQ = .5,
      BASE_OMEGA = -1 * Math.PI / 10,
      COLLECTION_RATIO = .01,
      HOLD_RATIO = .2,
      radiusPow = 2.5,
      rCore = .25,
      rOuter = rVortex,
      vIn = .9,
      COLLAPSE_TO_CORE = false,
      BURST_EXPANSION = .1,
      FADE_DURATION = 1.5,
      MAX_FADE_DELAY = 3,
      MAX_ASCEND_DELAY = 10,
      apexY = maxY,
      LOW_REGION_FACTOR = .5;

    let minBottomY = Infinity,
      maxBottomY = -Infinity;
    for (let i = 1; i < bottomPositions.length; i += 3) {
      const y = bottomPositions[i];
      if (y < minBottomY) minBottomY = y;
      if (y > maxBottomY) maxBottomY = y;
    }

    const Y_THRESHOLD = minBottomY + .5 * (maxBottomY - minBottomY),
      LOW_HEIGHT_MULTI = 2;

    {
      const tempPositions = [],
        tempColors = [],
        tempSizes = [];
      for (let i = 0; i < bottomPositions.length; i += 3) {
        const y = bottomPositions[i + 1];
        if (y >= Y_THRESHOLD) {
          for (let j = 1; j < 2; j++) {
            tempPositions.push(bottomPositions[i], y, bottomPositions[i + 2]);
            tempColors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
            tempSizes.push(bottomSizes[i / 3]);
          }
        }
      }
      bottomPositions.push(...tempPositions);
      bottomColors.push(...tempColors);
      bottomSizes.push(...tempSizes);
    }

    const BOTTOM_ROTATION_RATIO = .2,
      rotPos = [],
      rotColors = [],
      rotSizes = [],
      staticBotPos = [],
      staticBotColors = [],
      staticBotSizes = [];

    for (let i = 0; i < bottomPositions.length; i += 3) {
      if (Math.random() < .2) {
        rotPos.push(bottomPositions[i], bottomPositions[i + 1], bottomPositions[i + 2]);
        rotColors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
        rotSizes.push(bottomSizes[i / 3]);
      } else {
        staticBotPos.push(bottomPositions[i], bottomPositions[i + 1], bottomPositions[i + 2]);
        staticBotColors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
        staticBotSizes.push(bottomSizes[i / 3]);
      }
    }
    bottomPositions.length = 0;
    bottomPositions.push(...rotPos);
    bottomColors.length = 0;
    bottomColors.push(...rotColors);
    bottomSizes.length = 0;
    bottomSizes.push(...rotSizes);

    const bottomCount = bottomPositions.length / 3,
      bottomRadiusArr = new Float32Array(bottomCount),
      bottomPhaseArr = new Float32Array(bottomCount),
      bottomDelayArr = new Float32Array(bottomCount),
      INDENT_FACTOR = 2.5,
      bottomAlphaArr = new Float32Array(bottomCount).fill(1),
      bottomIsLow = new Uint8Array(bottomCount),
      pivotOffset = .25 * heartWidth,
      MIN_HOLD_LOW = 0,
      MAX_HOLD_LOW = .3;

    for (let i = 0; i < bottomCount; i++) {
      const x = bottomPositions[3 * i];
      const y = bottomPositions[3 * i + 1];
      const z = bottomPositions[3 * i + 2];
      const isLow = y < Y_THRESHOLD;
      bottomIsLow[i] = isLow ? 1 : 0;
      if (isLow) {
        const prob = 0 + (y - minBottomY) / (Y_THRESHOLD - minBottomY) * .3;
        bottomAlphaArr[i] = Math.random() < prob ? 1 : 0;
      } else {
        bottomAlphaArr[i] = 1;
      }
      const radius = Math.sqrt(x * x + z * z);
      const phase = Math.atan2(z, x);
      const indentFactor = Math.min(1, Math.abs(x) / (.25 * heartWidth));
      const scale = 1.5 * Math.pow(1 - indentFactor, 3) + 1;
      bottomRadiusArr[i] = radius * scale;
      bottomPhaseArr[i] = phase;
      bottomDelayArr[i] = 10 * Math.random();
    }

    const bottomAlphaBase = Float32Array.from(bottomAlphaArr),
      bottomGeo = new THREE.BufferGeometry();

    bottomGeo.setAttribute("position", new THREE.Float32BufferAttribute(bottomPositions, 3));
    bottomGeo.setAttribute("color", new THREE.Float32BufferAttribute(bottomColors, 3).setUsage(THREE.DynamicDrawUsage));
    bottomGeo.setAttribute("size", new THREE.Float32BufferAttribute(bottomSizes, 1));
    bottomGeo.setAttribute("alpha", new THREE.BufferAttribute(bottomAlphaArr, 1));

    const V_SLOPE = .3,
      matBottom = makeMat({
        map: circleTexture,
        alphaSupport: true,
        vClipSlope: .3,
        clipFrontZ: .3
      });
    matBottom.alphaTest = .5;

    const bottomHeart = new THREE.Points(bottomGeo, matBottom);
    bottomHeart.rotation.z = Math.PI;
    bottomHeart.renderOrder = 0;
    scene.add(bottomHeart);

    const BOTTOM_OMEGA = BASE_OMEGA,
      topPointVisibility = new Array(topIndices.length).fill(true);
    let hiddenTopCount = 0;

    const matStatic = makeMat({
      map: circleTexture,
      alphaSupport: true
    });
    matStatic.alphaTest = .5;

    const staticHeart = new THREE.Points(staticGeo, matStatic);
    staticHeart.rotation.z = Math.PI;
    staticHeart.renderOrder = 0;
    scene.add(staticHeart);

    const TOP_STATIC_RATIO = .5;

    {
      const tempPositions = [],
        tempColors = [],
        tempSizes = [];
      for (let i = 0; i < topPositionsArr.length; i += 3) {
        const isEdge = calculateMinDistanceToBorder(topPositionsArr[i] + 5, topPositionsArr[i + 1] + 7) < BORDER_THRESHOLD || Math.random() < .3;
        if (Math.random() < .5 && isEdge) {
          tempPositions.push(topPositionsArr[i], topPositionsArr[i + 1], topPositionsArr[i + 2]);
          tempColors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
          tempSizes.push(topSizes[Math.floor(i / 3)]);
        }
      }
      if (tempPositions.length > 0) {
        const geo = new THREE.BufferGeometry();
        geo.setAttribute("position", new THREE.Float32BufferAttribute(tempPositions, 3));
        geo.setAttribute("color", new THREE.Float32BufferAttribute(tempColors, 3).setUsage(THREE.DynamicDrawUsage));
        geo.setAttribute("size", new THREE.Float32BufferAttribute(tempSizes, 1));
        const mat = makeMat({
          map: circleTexture,
          alphaSupport: true
        });
        mat.alphaTest = .5;
        staticTopHeart = new THREE.Points(geo, mat);
        staticTopHeart.rotation.z = Math.PI;
        staticTopHeart.renderOrder = 0;
        scene.add(staticTopHeart);
      }
    }

    if (staticBotPos.length > 0) {
      const geo = new THREE.BufferGeometry();
      geo.setAttribute("position", new THREE.Float32BufferAttribute(staticBotPos, 3));
      geo.setAttribute("color", new THREE.Float32BufferAttribute(staticBotColors, 3).setUsage(THREE.DynamicDrawUsage));
      geo.setAttribute("size", new THREE.Float32BufferAttribute(staticBotSizes, 1));
      const mat = makeMat({
        map: circleTexture,
        alphaSupport: true
      });
      mat.alphaTest = .5;
      staticBottomHeart = new THREE.Points(geo, mat);
      staticBottomHeart.rotation.z = Math.PI;
      staticBottomHeart.renderOrder = 0;
      scene.add(staticBottomHeart);
    }

    const SPAWN_MULT = .2,
      rimIndices = [];
    for (const idx of topIndices) {
      if (calculateMinDistanceToBorder(positions[3 * idx], positions[3 * idx + 1]) < BORDER_THRESHOLD) {
        rimIndices.push(idx);
      }
    }

    const streamSource = rimIndices.length ? rimIndices : topIndices,
      streamCount = Math.floor(.2 * streamSource.length),
      targetIdxArr = new Uint32Array(streamCount);

    for (let i = 0; i < streamCount; i++) {
      targetIdxArr[i] = streamSource[i % streamSource.length];
    }

    const planeIdxForStream = new Int32Array(streamCount).fill(-1),
      streamPositions = new Float32Array(3 * streamCount),
      streamGeo = new THREE.BufferGeometry(),
      streamAlpha = new Float32Array(streamCount).fill(1);

    streamGeo.setAttribute("alpha", new THREE.BufferAttribute(streamAlpha, 1));
    streamGeo.setAttribute("position", new THREE.BufferAttribute(streamPositions, 3).setUsage(THREE.DynamicDrawUsage));

    const streamColors = new Float32Array(3 * streamCount);
    for (let i = 0; i < streamCount; i++) {
      streamColors[3 * i] = heartInitialColor.r;
      streamColors[3 * i + 1] = heartInitialColor.g;
      streamColors[3 * i + 2] = heartInitialColor.b;
    }
    streamGeo.setAttribute("color", new THREE.BufferAttribute(streamColors, 3));

    const streamSizes = new Float32Array(streamCount);
    for (let i = 0; i < streamCount; i++) {
      streamSizes[i] = 2 * (.3 * Math.random() + .2 + .1) * 1.5;
    }
    const streamSizeBase = streamSizes.slice(),
      GRAN_RATIO = .1;

    for (let i = 0; i < streamCount; i++) {
      if (Math.random() < .1) {
        streamSizes[i] *= 1.5;
        streamColors[3 * i] = heartInitialColor.r;
        streamColors[3 * i + 1] = heartInitialColor.g;
        streamColors[3 * i + 2] = heartInitialColor.b;
      }
    }
    streamGeo.setAttribute("size", new THREE.BufferAttribute(streamSizes, 1));

    const matStream = makeMat({
      map: circleTexture,
      alphaSupport: true,
      indentWidth: INDENT_HALF_WIDTH,
      clipFrontZ: .3
    });
    matStream.alphaTest = .5;

    const streamHeart = new THREE.Points(streamGeo, matStream);
    streamHeart.rotation.z = Math.PI;
    streamHeart.renderOrder = 1;
    scene.add(streamHeart);
    streamHeart.visible = false;
    fadeObjects.push(streamHeart);
    streamHeart.userData.fadeStage = STAGE.STREAM;

    const PLANE_COUNT = Math.floor(120 * rVortex),
      planePositions = [],
      planeColors = [],
      planeSizes = [],
      planeAlphaArr = new Float32Array(PLANE_COUNT).fill(1);

    for (let i = 0; i < PLANE_COUNT; i++) {
      const angle = Math.random() * Math.PI * 2;
      const radius = Math.sqrt(Math.random()) * rVortex;
      planePositions.push(Math.cos(angle) * radius, planeYCenter - 7.5, Math.sin(angle) * radius);
      planeColors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
      planeSizes.push(1 * Math.random() + .25);
    }

    const planeGeo = new THREE.BufferGeometry();
    planeGeo.setAttribute("position", new THREE.Float32BufferAttribute(planePositions, 3));
    planeGeo.setAttribute("color", new THREE.Float32BufferAttribute(planeColors, 3));
    planeGeo.setAttribute("size", new THREE.Float32BufferAttribute(planeSizes, 1));
    planeGeo.setAttribute("alpha", new THREE.BufferAttribute(planeAlphaArr, 1));

    const matPlane = makeMat({
      map: circleTexture,
      alphaSupport: true
    });
    matPlane.alphaTest = .5;

    const planeLayer = new THREE.Points(planeGeo, matPlane);
    planeLayer.rotation.z = Math.PI;
    scene.add(planeLayer);
    fadeObjects.push(planeLayer);
    if (fadeObjects.includes(planeLayer)) {
      fadeObjects.splice(fadeObjects.indexOf(planeLayer), 1);
    }
    planeLayer.visible = true;

    const PLANE_COLOR_CYCLE = 9,
      PLANE_COL_WHITE = new THREE.Color("rgb(255, 227, 249)"),
      PLANE_COL_LIGHT = new THREE.Color("rgb(255,192,215)"),
      PLANE_COL_DARK = new THREE.Color("rgb(241, 121, 185)");

    function createTextSpriteTexture(char) {
      const canvas = document.createElement("canvas");
      canvas.width = canvas.height = 128;
      const ctx = canvas.getContext("2d");
      ctx.fillStyle = "rgba(0,0,0,0)";
      ctx.fillRect(0, 0, 128, 128);
      ctx.textAlign = "center";
      ctx.textBaseline = "middle";
      ctx.font = '300 70.4px "Quicksand","Comfortaa","Segoe UI Emoji","Noto Color Emoji","Apple Color Emoji",sans-serif';
      ctx.lineWidth = 7.68;
      ctx.strokeStyle = "rgba(160, 30, 95, 0.9)";
      ctx.strokeText(char, 64, 64);
      ctx.fillStyle = "#ffffff";
      ctx.fillText(char, 64, 64);
      const texture = new THREE.CanvasTexture(canvas);
      texture.minFilter = texture.magFilter = THREE.LinearFilter;
      return texture;
    }

    planeGeo.attributes.color.setUsage(THREE.DynamicDrawUsage);

    const ringCharsFull = RingText.join(""),
      ringChars = Array.from(ringCharsFull),
      charMatMap = {};

    function generateTextRingTexture(lines) {
      const canvas = document.createElement("canvas");
      canvas.width = 2048; canvas.height = 256;
      const ctx = canvas.getContext("2d");
      ctx.fillStyle = "rgba(0,0,0,0)";
      ctx.fillRect(0, 0, canvas.width, canvas.height);
      ctx.font = 'bold 80px "Noto Sans", "Noto Sans JP", "Noto Sans KR", "Noto Sans SC", "Noto Sans TC", "Noto Sans Arabic", "Noto Sans Devanagari", "Noto Sans Hebrew", "Noto Sans Thai", sans-serif';
      ctx.textAlign = "center";
      ctx.textBaseline = "middle";
      const lineHeight = canvas.height / lines.length;
      lines.forEach((textLine, index) => {
        const y = (index + 0.5) * lineHeight;
        ctx.shadowColor = '#ff40c8';
        ctx.shadowBlur = 0;
        ctx.fillStyle = '#ff40c8';
        ctx.fillText(textLine, canvas.width / 2, y);
        ctx.shadowBlur = 0;
        ctx.strokeStyle = "rgba(160, 30, 95, 0.9)";
        ctx.lineWidth = 3;
        ctx.strokeText(textLine, canvas.width / 2, y);
        ctx.fillStyle = "#ffffff";
        ctx.fillText(textLine, canvas.width / 2, y);
      });
      const texture = new THREE.CanvasTexture(canvas);
      texture.needsUpdate = true;
      return texture;
    }

    [...new Set(ringChars)].forEach(char => {
      charMatMap[char] = new THREE.SpriteMaterial({
        map: createTextSpriteTexture(char),
        transparent: true,
        depthWrite: false
      });
    });

    const ringTexture = generateTextRingTexture(RingText),
      ringMat = new THREE.MeshBasicMaterial({
        map: ringTexture,
        transparent: true,
        side: THREE.DoubleSide,
        depthWrite: false,
        blending: THREE.AdditiveBlending
      }),
      RING_THICKNESS = 3.5,
      RING_TONE_SPEED = .05,
      RING_FADE_DIST = 1,
      RING_FADE_SPEED = 2,
      RING_HEIGHT = .8,
      RING_Y_OFFSET = 2 * -planeYCenter - .5,
      ringGeo = new THREE.CylinderGeometry(rVortex, rVortex, 1, 128, 1, true),
      RING_SPACING = 2,
      RING_START_RADIUS = rVortex,
      RING_END_RADIUS = .25,
      RING_COUNT = Math.ceil((RING_START_RADIUS - .25) / 2),
      RING_FLIP_Y = Math.PI,
      ribbon = new THREE.Group();

    ribbon.position.set(0, planeYCenter + RING_Y_OFFSET, 0);
    ribbon.rotation.z = Math.PI;
    scene.add(ribbon);
    ribbon.visible = true;

    for (let i = 0; i < RING_COUNT; i++) {
      const texture = generateTextRingTexture([RingText[i % RingText.length]]);
      texture.wrapS = THREE.RepeatWrapping;
      texture.repeat.set(2, 1);
      texture.offset.x = 1;
      const material = new THREE.MeshBasicMaterial({
        map: texture,
        transparent: true,
        side: THREE.DoubleSide,
        depthWrite: false,
        blending: THREE.AdditiveBlending
      });
      const mesh = new THREE.Mesh(ringGeo, material);
      mesh.rotation.x = Math.PI;
      const radius = RING_START_RADIUS - 2 * i;
      const jitter = 2 * (Math.random() - .5) * .3;
      mesh.userData.radius = radius + jitter;
      mesh.userData.phase = Math.random() * Math.PI * 2;
      const scale = radius / RING_START_RADIUS;
      mesh.scale.set(scale, 3.5, scale);
      mesh.material.opacity = 1;
      mesh.material.transparent = true;
      mesh.material.depthWrite = false;
      mesh.renderOrder = i;
      ribbon.add(mesh);
    }

    const vortexIndices = [];
    for (let i = 0; i < positions.length / 3; i++) {
      if (!topIndices.includes(i)) {
        vortexIndices.push(i);
      }
    }

    const vortexCount = vortexIndices.length,
      vortexPositions = new Float32Array(3 * vortexCount),
      vortexPhase = new Float32Array(vortexCount),
      vortexRadius = new Float32Array(vortexCount);

    for (let i = 0; i < vortexCount; i++) {
      vortexPhase[i] = Math.random() * Math.PI * 2;
      const radius = Math.random() * rVortex;
      vortexRadius[i] = radius;
      vortexPositions[3 * i] = Math.cos(vortexPhase[i]) * radius;
      vortexPositions[3 * i + 1] = planeYCenter;
      vortexPositions[3 * i + 2] = Math.sin(vortexPhase[i]) * radius;
    }

    const vortexGeo = new THREE.BufferGeometry();
    vortexGeo.setAttribute("position", new THREE.BufferAttribute(vortexPositions, 3).setUsage(THREE.DynamicDrawUsage));

    const vortexColors = new Float32Array(3 * vortexCount);
    for (let i = 0; i < vortexCount; i++) {
      vortexColors[3 * i] = heartInitialColor.r;
      vortexColors[3 * i + 1] = heartInitialColor.g;
      vortexColors[3 * i + 2] = heartInitialColor.b;
    }
    vortexGeo.setAttribute("color", new THREE.BufferAttribute(vortexColors, 3));

    const vortexSizes = new Float32Array(vortexCount);
    for (let i = 0; i < vortexCount; i++) {
      vortexSizes[i] = .2 * Math.random() + .15;
    }
    vortexGeo.setAttribute("size", new THREE.BufferAttribute(vortexSizes, 1));

    const vortexMat = makeMat({
      map: circleTexture,
      blending: THREE.AdditiveBlending,
      opacity: .8
    });
    vortexMat.onBeforeCompile = function (shader) {
      shader.vertexShader = shader.vertexShader.replace("uniform float pointSize;", "attribute float pointSize;");
    };

    const heartLayers = [staticHeart, bottomHeart, staticBottomHeart, staticTopHeart];
    heartLayers.forEach(layer => {
      if (layer) {
        scene.remove(layer);
        heartScene.add(layer);
      }
    });
    heartLayers.forEach(layer => {
      if (layer) {
        layer.visible = false;
        layer.userData.fadeStage = STAGE.HEART;
        if (!fadeObjects.includes(layer)) fadeObjects.push(layer);
      }
    });

    const HEART_OFFSET_Y = 10;
    [staticHeart, bottomHeart, staticTopHeart, staticBottomHeart].forEach(layer => {
      if (layer) layer.position.y += 10;
    });

    const HEART_OFFSET_YY = 8;
    [streamHeart, ribbon].forEach(group => {
      if (group) group.position.y += 8;
    });

    const ENABLE_EXPLOSION = false;
    let expPositions, expVelocities, expBirth, expGeo, expColors, expMat, explosionPoints, MAX_EXP, expCount = 0;

    const startTimes = new Float32Array(streamCount),
      STATE_ON_DISK = 0,
      STATE_ASCEND = 1,
      streamState = new Uint8Array(streamCount),
      curRadiusArr = new Float32Array(streamCount),
      ascendStart = new Float32Array(streamCount),
      spiralPhase = new Float32Array(streamCount),
      streamRadius = new Float32Array(streamCount),
      initialRadius = new Float32Array(streamCount),
      spiralFrequency = new Float32Array(streamCount),
      spiralDirection = new Float32Array(streamCount),
      extraRotArr = new Float32Array(streamCount),
      MAX_TOP_HIDE = Math.floor(1 * topIndices.length),
      HIDE_DISTANCE = .25,
      TOP_ROTATION_SPEED = .5,
      streamRiseDuration = new Float32Array(streamCount),
      streamOffsets = new Float32Array(3 * streamCount);

    for (let i = 0; i < streamCount; i++) {
      const idx = 3 * i;
      const angle = Math.random() * Math.PI * 2;
      const phi = Math.acos(2 * Math.random() - 1);
      const jitter = .4;
      streamOffsets[idx] = jitter * Math.sin(phi) * Math.cos(angle);
      streamOffsets[idx + 1] = jitter * Math.sin(phi) * Math.sin(angle);
      streamOffsets[idx + 2] = jitter * Math.cos(phi);
    }

    function initializeStreamParticleState(index, currentTime) {
      const posIdx = 3 * index;
      const targetIndex = targetIdxArr[index];
      let planeIndex = -1;
      for (let attempt = 0; attempt < 100; attempt++) {
        const randomPlaneIdx = Math.floor(Math.random() * PLANE_COUNT);
        const x = planePositions[3 * randomPlaneIdx];
        const z = planePositions[3 * randomPlaneIdx + 2];
        if (Math.hypot(x, z) <= .26) {
          planeIndex = randomPlaneIdx;
          break;
        }
      }
      if (planeIndex === -1) planeIndex = Math.floor(Math.random() * PLANE_COUNT);
      planeIdxForStream[index] = planeIndex;

      const randomAngle = Math.random() * Math.PI * 2;
      planePositions[3 * planeIndex] = Math.cos(randomAngle) * rOuter;
      planePositions[3 * planeIndex + 2] = Math.sin(randomAngle) * rOuter;
      planeGeo.attributes.position.needsUpdate = true;

      const layerRotation = planeLayer.rotation.y;
      const cosRot = Math.cos(layerRotation);
      const sinRot = Math.sin(layerRotation);
      const rotatedX = cosRot * planePositions[3 * planeIndex] - sinRot * planePositions[3 * planeIndex + 2];
      const rotatedZ = sinRot * planePositions[3 * planeIndex] + cosRot * planePositions[3 * planeIndex + 2];

      streamPositions[posIdx] = rotatedX;
      streamPositions[posIdx + 1] = planePositions[3 * planeIndex + 1];
      streamPositions[posIdx + 2] = rotatedZ;

      const spawnRadius = .25 + (rOuter - .25) * Math.random();
      const spawnAngle = Math.random() * Math.PI * 2;
      streamPositions[posIdx] = Math.cos(spawnAngle) * spawnRadius;
      streamPositions[posIdx + 1] = planeYCenter;
      streamPositions[posIdx + 2] = Math.sin(spawnAngle) * spawnRadius;
      curRadiusArr[index] = spawnRadius;
      spiralPhase[index] = spawnAngle;
      streamState[index] = STATE_ON_DISK;
      startTimes[index] = currentTime - Math.random() * (rOuter - .25) / .9;
      ascendStart[index] = 10 * Math.random();
      streamRiseDuration[index] = 8 + 4 * Math.random();

      const extraRotSpeed = .5 + 1.5 * Math.random();
      const extraRotDir = Math.random() < .5 ? -1 : 1;
      extraRotArr[index] = 2 * extraRotSpeed * Math.PI * extraRotDir;

      const topIdx = idxToTopIdx[targetIndex];
      if (topIdx !== -1) {
        topAlpha[topIdx] = 1;
        staticGeo.attributes.alpha.needsUpdate = true;
      }
      if (activeImages.has(index)) releaseImageToPool(index);
      if (activeTexts.has(index)) releaseTextToPool(index);
      streamAlpha[index] = 1;
      streamGeo.attributes.alpha.needsUpdate = true;
    }

    const now0 = 0;
    for (let i = 0; i < streamCount; i++) {
      initializeStreamParticleState(i, 0);
    }
    streamGeo.attributes.position.needsUpdate = true;
    streamGeo.attributes.alpha.needsUpdate = true;

    const clock = new THREE.Clock();
    let initialColorApplied = false;

    function mainAnimationLoop() {
      requestAnimationFrame(mainAnimationLoop);
      let delta = clock.getDelta();
      const elapsedTime = clock.getElapsedTime();
      if (delta > 0.1) delta = 0.1;

      for (let i = 0; i < PLANE_COUNT; i++) {
        const idx = 3 * i;
        let x = planePositions[idx];
        let z = planePositions[idx + 2];
        let radius = Math.hypot(x, z);
        if (radius > .25) {
          radius = Math.max(.25, radius - .9 * delta);
          const angle = Math.atan2(z, x);
          planePositions[idx] = Math.cos(angle) * radius;
          planePositions[idx + 2] = Math.sin(angle) * radius;
        }
      }
      planeGeo.attributes.position.needsUpdate = true;

      if (planeLayer.visible) {
        planeLayer.rotation.y = BASE_OMEGA * elapsedTime;
      }
      if (ribbon && ribbon.children.length) {
        ribbon.rotation.y = planeLayer.rotation.y + RING_FLIP_Y;
        const radiusRange = RING_START_RADIUS - .25;
        ribbon.children.forEach((child, index) => {
          child.userData.radius -= .9 * delta;
          if (child.userData.radius - 1.75 < .25) {
            child.userData.radius += radiusRange + 2;
          }
          const currentRadius = child.userData.radius - 1.75;
          if (currentRadius < 1.25) {
            const t = THREE.MathUtils.clamp((currentRadius - .25) / 1, 0, 1);
            child.material.opacity = t;
          }
          if (currentRadius < .25) {
            child.userData.radius += radiusRange + 2;
            child.material.opacity = 0;
          }
          if (child.material.opacity < 1) {
            child.material.opacity = Math.min(1, child.material.opacity + 2 * delta);
          }
          const scale = child.userData.radius / RING_START_RADIUS;
          child.scale.set(scale, 3.5, scale);
          child.material.color.set(0xffffff);
          child.rotation.y = child.userData.phase;
        });
      }

      camera.updateMatrixWorld();

      if (streamHeartStarted) {
        const currentTimeMs = 1000 * elapsedTime;
        controlImageSpawningLogic(currentTimeMs);
        handleQueuedImageSpawns();
        animateFloatingImageSprites(currentTimeMs);
        if (currentTimeMs - lastStatusLogTime > 3000) {
          printImageSystemReport();
          lastStatusLogTime = currentTimeMs;
        }

        for (let i = 0; i < streamCount; i++) {
          const posIdx = 3 * i;
          const startTime = startTimes[i];
          const timeSinceStart = elapsedTime - (startTime + i % 5 * 1.6);
          const targetIndex = targetIdxArr[i];

          if (streamState[i] === STATE_ON_DISK) {
            const currentPhase = spiralPhase[i] + BASE_OMEGA * (elapsedTime - startTime);
            streamPositions[posIdx] = Math.cos(currentPhase) * curRadiusArr[i];
            streamPositions[posIdx + 1] = planeYCenter;
            streamPositions[posIdx + 2] = Math.sin(currentPhase) * curRadiusArr[i];
            if (activeImages.has(i)) releaseImageToPool(i);
            streamAlpha[i] = 1;
            if (timeSinceStart >= ascendStart[i]) {
              streamState[i] = STATE_ASCEND;
              startTimes[i] = elapsedTime;
              initialRadius[i] = curRadiusArr[i];
            }
            continue;
          }

          if (timeSinceStart < -1.5) {
            const phase = spiralPhase[i] + BASE_OMEGA * (elapsedTime - startTime);
            streamPositions[posIdx] = initialRadius[i] * Math.cos(phase);
            streamPositions[posIdx + 1] = planeYCenter;
            streamPositions[posIdx + 2] = initialRadius[i] * Math.sin(phase);
            streamAlpha[i] = 0;
            continue;
          }

          if (timeSinceStart < 0) {
            const fadeInProgress = (timeSinceStart + 1.5) / 1.5;
            const easeIn = fadeInProgress * fadeInProgress * (3 - 2 * fadeInProgress);
            streamAlpha[i] = easeIn;
            if (activeImages.has(i)) releaseImageToPool(i);
            const phase = spiralPhase[i] + BASE_OMEGA * (elapsedTime - startTime);
            streamPositions[posIdx] = initialRadius[i] * Math.cos(phase);
            streamPositions[posIdx + 1] = planeYCenter;
            streamPositions[posIdx + 2] = initialRadius[i] * Math.sin(phase);
            continue;
          }

          const riseDuration = streamRiseDuration[i];
          if (timeSinceStart >= riseDuration) {
            const fadeOutProgress = (timeSinceStart - riseDuration) / 1.5;
            if (fadeOutProgress < 1) {
              const easeOut = 1 - fadeOutProgress * fadeOutProgress * (3 - 2 * fadeOutProgress);
              streamAlpha[i] = 1 - fadeOutProgress;
              if (activeImages.has(i)) {
                const poolIdx = activeImages.get(i);
                imagePool[poolIdx].material.opacity *= 1 - fadeOutProgress;
              }
              const phase = spiralPhase[i] + BASE_OMEGA * (elapsedTime - startTime);
              streamPositions[posIdx] = initialRadius[i] * Math.cos(phase);
              streamPositions[posIdx + 1] = planeYCenter;
              streamPositions[posIdx + 2] = initialRadius[i] * Math.sin(phase);
              continue;
            }
            streamAlpha[i] = 1;
            if (activeImages.has(i)) releaseImageToPool(i);
            initializeStreamParticleState(i, elapsedTime);
            if (!firstResetCompleted) firstResetCompleted = true;
            continue;
          }

          streamAlpha[i] = 1;
          const normalizedTime = timeSinceStart / riseDuration;

          if (normalizedTime < .01) {
            let targetX, targetY, targetZ;
            const currentPhase = spiralPhase[i] + BASE_OMEGA * (elapsedTime - startTime);
            {
              const rad = initialRadius[i];
              targetX = Math.cos(currentPhase) * rad;
              targetZ = Math.sin(currentPhase) * rad;
              const t = normalizedTime / .01;
              targetY = THREE.MathUtils.lerp(planeYCenter, apexY, t);
            }
            streamPositions[posIdx] = targetX;
            streamPositions[posIdx + 1] = targetY;
            streamPositions[posIdx + 2] = targetZ;
          } else {
            const easedTime = (normalizedTime - .01) / .99;
            const easeOutCubic = 1 - Math.pow(1 - easedTime, 3);
            const currentPhase = spiralPhase[i] + BASE_OMEGA * (elapsedTime - startTime);
            const startRadius = initialRadius[i];
            const startX = Math.cos(currentPhase) * startRadius;
            const startZ = Math.sin(currentPhase) * startRadius;
            const startY = apexY;
            const targetIdx3 = 3 * targetIndex;
            const targetX = positions[targetIdx3];
            const targetY = positions[targetIdx3 + 1] - 4 + 2;
            const targetZ = positions[targetIdx3 + 2];
            let finalX = THREE.MathUtils.lerp(startX, targetX, easeOutCubic);
            let finalY = THREE.MathUtils.lerp(startY, targetY, easeOutCubic);
            let finalZ = THREE.MathUtils.lerp(startZ, targetZ, easeOutCubic);
            const scale = 1 + .1 * (1 - easeOutCubic);
            finalX *= scale;
            finalZ *= scale;
            const extraRot = (1 - easeOutCubic) * extraRotArr[i];
            const cosExtra = Math.cos(extraRot);
            const sinExtra = Math.sin(extraRot);
            const rotatedX = finalX * cosExtra - finalZ * sinExtra;
            const rotatedZ = finalX * sinExtra + finalZ * cosExtra;
            streamPositions[posIdx] = rotatedX;
            streamPositions[posIdx + 1] = finalY;
            streamPositions[posIdx + 2] = rotatedZ;
          }

          if (normalizedTime < .01) {
            streamAlpha[i] = 1;
            if (activeImages.has(i)) releaseImageToPool(i);
          } else {
            const easedTime = (normalizedTime - .01) / .99;
            let imageSprite = null;
            if (activeImages.has(i)) {
              const poolIdx = activeImages.get(i);
              imageSprite = imagePool[poolIdx];
            }
            if (imageSprite) {
              streamAlpha[i] = 0;
              imageSprite.visible = true;
              const easeOutCubic = 1 - Math.pow(1 - easedTime, 3);
              const targetIdx3 = 3 * targetIndex;
              const targetX = positions[targetIdx3];
              const targetY = positions[targetIdx3 + 1] - 4 + 2;
              const targetZ = positions[targetIdx3 + 2];
              const orbitSpeed = 1 + i % 5 * .2;
              const orbitDir = i % 2 === 0 ? 1 : -1;
              const orbitAngle = currentPhase + easeOutCubic * orbitSpeed * Math.PI * 2 * orbitDir;
              const orbitRadius = (1 - easeOutCubic) * (2 + 1 * Math.sin(i));
              const easedX = THREE.MathUtils.lerp(0, targetX, easeOutCubic);
              const easedY = THREE.MathUtils.lerp(apexY, targetY, easeOutCubic);
              const easedZ = THREE.MathUtils.lerp(0, targetZ, easeOutCubic);
              const finalX = easedX + Math.cos(orbitAngle) * orbitRadius;
              const finalY = easedY;
              const finalZ = easedZ + Math.sin(orbitAngle) * orbitRadius;
              imageSprite.position.set(finalX, finalY, finalZ);
              if (easedTime > .4) {
                const fadeOut = (easedTime - .4) / .6;
                imageSprite.material.opacity = 1 * (1 - fadeOut);
                const scaleMultiplier = 1 - .9 * fadeOut;
                const aspect = imageSprite.userData.aspectScale || { x: IMAGE_CONFIG.scale, y: IMAGE_CONFIG.scale };
                imageSprite.scale.set(aspect.x * scaleMultiplier, aspect.y * scaleMultiplier, 1);
                if (fadeOut > .9) {
                  imageSprite.visible = false;
                  releaseImageToPool(i);
                }
              } else {
                imageSprite.material.opacity = 1;
                const aspect = imageSprite.userData.aspectScale || { x: IMAGE_CONFIG.scale, y: IMAGE_CONFIG.scale };
                imageSprite.scale.set(aspect.x, aspect.y, 1);
              }
            } else {
              streamAlpha[i] = 1;
            }
          }

          if (normalizedTime > .95) {
            const topIdx = topIndices.indexOf(targetIndex);
            if (topPointVisibility[topIdx] && hiddenTopCount < MAX_TOP_HIDE) {
              topPointVisibility[topIdx] = false;
              const mappedIdx = idxToTopIdx[targetIndex];
              if (mappedIdx !== -1) {
                topAlpha[mappedIdx] = 0;
                staticGeo.attributes.alpha.needsUpdate = true;
              }
              hiddenTopCount++;
            }
          }
        }
      } else {
        for (let i = 0; i < streamCount; i++) {
          if (streamHeartActiveRatio < 1 && i / streamCount > .1) {
            const posIdx = 3 * i;
            const phase = spiralPhase[i] + BASE_OMEGA * elapsedTime;
            streamPositions[posIdx] = Math.cos(phase) * curRadiusArr[i];
            streamPositions[posIdx + 1] = planeYCenter;
            streamPositions[posIdx + 2] = Math.sin(phase) * curRadiusArr[i];
            streamAlpha[i] = 0;
            continue;
          }
          if (!firstResetCompleted && i / streamCount > 1e-4) {
            const posIdx = 3 * i;
            const phase = spiralPhase[i] + BASE_OMEGA * elapsedTime;
            streamPositions[posIdx] = Math.cos(phase) * curRadiusArr[i];
            streamPositions[posIdx + 1] = planeYCenter;
            streamPositions[posIdx + 2] = Math.sin(phase) * curRadiusArr[i];
            streamAlpha[i] = 0;
            continue;
          }
          const posIdx = 3 * i;
          const phase = spiralPhase[i] + BASE_OMEGA * elapsedTime;
          streamPositions[posIdx] = Math.cos(phase) * curRadiusArr[i];
          streamPositions[posIdx + 1] = planeYCenter;
          streamPositions[posIdx + 2] = Math.sin(phase) * curRadiusArr[i];
          streamAlpha[i] = 0;
        }
        streamGeo.attributes.position.needsUpdate = true;
        streamGeo.attributes.alpha.needsUpdate = true;
      }

      streamGeo.attributes.position.needsUpdate = true;
      streamGeo.attributes.alpha.needsUpdate = true;

      for (let i = 0; i < vortexCount; i++) {
        const posIdx = 3 * i;
        const omega = 1 * Math.PI / 10;
        const baseRadius = vortexRadius[i];
        const timeOffset = elapsedTime * omega;
        const radialJitter = .3 * Math.sin(timeOffset + vortexPhase[i]);
        const angularJitter = .2 * Math.cos(.7 * timeOffset + vortexPhase[i]);
        const currentPhase = timeOffset + vortexPhase[i] + radialJitter;
        const modulatedRadius = baseRadius * (1 + angularJitter);
        vortexPositions[posIdx] = Math.cos(currentPhase) * modulatedRadius;
        vortexPositions[posIdx + 1] = planeYCenter + .5 * Math.sin(timeOffset + vortexPhase[i]);
        vortexPositions[posIdx + 2] = Math.sin(currentPhase) * modulatedRadius;
      }
      vortexGeo.attributes.position.needsUpdate = true;

      const bottomPositionsArr = bottomGeo.attributes.position.array;
      for (let i = 0; i < bottomCount; i++) {
        if (elapsedTime < bottomDelayArr[i]) continue;
        const phase = bottomPhaseArr[i];
        const radius = bottomRadiusArr[i];
        const x = Math.cos(phase) * radius;
        if (Math.abs(phase) < .25 * Math.PI) {
          const indentFactor = Math.min(1, Math.abs(x) / (.25 * heartWidth));
          const scale = 1.5 * Math.pow(1 - indentFactor, 3) + 1;
          const direction = x >= 0 ? 1 : -1;
          bottomPositionsArr[3 * i] = x + direction * (Math.abs(x) * (scale - 1));
        } else {
          bottomPositionsArr[3 * i] = x;
        }
        bottomPositionsArr[3 * i + 2] = Math.sin(phase) * radius;
        const currentX = bottomPositionsArr[3 * i];
        const currentY = bottomPositionsArr[3 * i + 1];
        const currentZ = bottomPositionsArr[3 * i + 2];
        const worldPos = new THREE.Vector3(currentX, currentY, currentZ).applyMatrix4(bottomHeart.matrixWorld);
        (new THREE.Vector3()).copy(worldPos).applyMatrix4(camera.matrixWorldInverse);
        bottomAlphaArr[i] = bottomAlphaBase[i];
      }
      bottomGeo.attributes.position.needsUpdate = true;
      bottomGeo.attributes.alpha.needsUpdate = true;

      const azimuthalAngle = controls.getAzimuthalAngle();
      if (staticHeart) staticHeart.rotation.y = azimuthalAngle;
      if (bottomHeart) bottomHeart.rotation.y = azimuthalAngle;
      if (staticBottomHeart) staticBottomHeart.rotation.y = azimuthalAngle;
      if (staticTopHeart) staticTopHeart.rotation.y = azimuthalAngle;

      if (heartbeatEnabled) {
        const pulse = 1 + .05 * Math.sin(.5 * elapsedTime * Math.PI * 2);
        if (staticHeart) staticHeart.scale.set(pulse, pulse, pulse);
        if (bottomHeart) bottomHeart.scale.set(pulse, pulse, pulse);
        if (staticBottomHeart) staticBottomHeart.scale.set(pulse, pulse, pulse);
        if (staticTopHeart) staticTopHeart.scale.set(pulse, pulse, pulse);
      }

      controls.update();
      renderer.clear();
      composerHeart.render();
      renderer.clearDepth();
      renderer.autoClear = false;
      composerMain.render();
      renderer.autoClear = true;

      if (hiddenTopCount < MAX_TOP_HIDE) {
        for (let i = 0; i < 5 && hiddenTopCount < MAX_TOP_HIDE; i++) {
          const randomTopIdx = Math.floor(Math.random() * topIndices.length);
          const globalIdx = topIndices[randomTopIdx];
          if (topPointVisibility[randomTopIdx]) {
            topPointVisibility[randomTopIdx] = false;
            const mappedIdx = idxToTopIdx[globalIdx];
            if (mappedIdx !== -1) {
              topAlpha[mappedIdx] = 0;
              hiddenTopCount++;
            }
          }
        }
        staticGeo.attributes.position.needsUpdate = true;
        staticGeo.attributes.alpha.needsUpdate = true;
      }

      for (let i = explosionEffects.length - 1; i >= 0; i--) {
        const group = explosionEffects[i];
        group.userData.life -= delta;
        if (group.userData.life <= 0) {
          if (!isPulsing) {
            isPulsing = true;
            pulseStartTime = elapsedTime;
            triggerCosmicRipple();
          }
          scene.remove(group);
          explosionEffects.splice(i, 1);
        } else {
          const points = group.children[0];
          const positions = points.geometry.attributes.position.array;
          const velocities = group.userData.velocities;
          const attractionForce = 0.04;
          for (let j = 0; j < velocities.length; j++) {
            const idx = j * 3;
            const currentPosition = new THREE.Vector3(positions[idx], positions[idx + 1], positions[idx + 2]);
            const currentVelocity = velocities[j];
            const toHeartVector = HEART_CENTER_TARGET.clone().sub(currentPosition);
            currentVelocity.lerp(toHeartVector, attractionForce);
            positions[idx] += currentVelocity.x * delta;
            positions[idx + 1] += currentVelocity.y * delta;
            positions[idx + 2] += currentVelocity.z * delta;
          }
          points.geometry.attributes.position.needsUpdate = true;
          if (group.userData.life < 1.0) {
            points.material.opacity = group.userData.life / 1.0;
          }
        }
      }

      const RIPPLE_LIFESPAN = 1.8;
      effectPool.waves.forEach(wave => {
        if (!wave.userData.active) return;
        const progress = (elapsedTime - wave.userData.creationTime) / RIPPLE_LIFESPAN;
        if (progress >= 1) {
          wave.userData.active = false;
          wave.visible = false;
        } else {
          wave.lookAt(camera.position);
          wave.scale.set(1 + progress * 6, 1 + progress * 6, 1);
          wave.material.opacity = 0.6 * (1 - progress);
        }
      });

      effectPool.sparkles.forEach(sparkles => {
        if (!sparkles.userData.active) return;
        const progress = (elapsedTime - sparkles.userData.creationTime) / RIPPLE_LIFESPAN;
        if (progress >= 1) {
          sparkles.userData.active = false;
          sparkles.visible = false;
        } else {
          const positions = sparkles.geometry.attributes.position.array;
          const velocities = sparkles.userData.velocities;
          for (let i = 0; i < 100; i++) {
            const idx = i * 3;
            positions[idx] += velocities[idx] * delta;
            positions[idx + 1] += velocities[idx + 1] * delta;
          }
          sparkles.geometry.attributes.position.needsUpdate = true;
          sparkles.material.opacity = 1 - Math.pow(progress, 2);
        }
      });

      if (streamHeartStarted && allWordsFlat.length > 0 && elapsedTime > nextWordSpawnTime) {
        const wordToSpawn = allWordsFlat[currentWordIndex];
        let foundParticle = -1;
        for (let i = 0; i < streamCount; i++) {
          const particleProgress = (elapsedTime - startTimes[i]) / streamRiseDuration[i];
          if (streamState[i] === STATE_ASCEND && particleProgress > 0 && particleProgress < 0.1 && !activeImages.has(i) && !activeTexts.has(i)) {
            foundParticle = i;
            break;
          }
        }
        if (foundParticle !== -1) {
          const textSprite = effectPool.texts.find(txt => !txt.userData.active && txt.userData.text === wordToSpawn);
          if (textSprite) {
            textSprite.userData.active = true;
            textSprite.userData.spawnTime = elapsedTime;
            textSprite.visible = true;
            textSprite.material.opacity = 0;
            activeTexts.set(foundParticle, textSprite);
            currentWordIndex = (currentWordIndex + 1) % allWordsFlat.length;
            nextWordSpawnTime = elapsedTime + WORD_SPAWN_INTERVAL;
          }
        }
      }

      activeTexts.forEach((sprite, particleIndex) => {
        const particleX = streamPositions[particleIndex * 3];
        const particleY = streamPositions[particleIndex * 3 + 1];
        const particleZ = streamPositions[particleIndex * 3 + 2];
        sprite.position.set(particleX, particleY + 1.5, particleZ);
        const lifeTime = elapsedTime - sprite.userData.spawnTime;
        const FADE_DURATION = 0.8;
        const particleProgress = (elapsedTime - startTimes[particleIndex]) / streamRiseDuration[particleIndex];
        if (lifeTime < FADE_DURATION) {
          sprite.material.opacity = lifeTime / FADE_DURATION;
        } else if (particleProgress > 0.7) {
          sprite.material.opacity = Math.max(0, 1 - (particleProgress - 0.7) / 0.3);
        } else {
          sprite.material.opacity = 1;
        }
        if (streamState[particleIndex] === STATE_ON_DISK || particleProgress >= 1.0) {
          releaseTextToPool(particleIndex);
        }
      });

      const heartMeshes = [staticHeart, bottomHeart, staticBottomHeart, staticTopHeart];
      let finalColor = new THREE.Color();
      if (useCustomColor) {
        finalColor.copy(heartInitialColor);
      } else {
        finalColor.setHSL((elapsedTime * 0.05) % 1, 0.8, 0.6);
      }

      if (isPulsing) {
        const pulseProgress = Math.min((elapsedTime - pulseStartTime) / PULSE_DURATION, 1.0);
        const pulseSine = Math.sin(pulseProgress * Math.PI);
        const scale = 1 + PULSE_AMPLITUDE * pulseSine;
        heartMeshes.forEach(mesh => { if (mesh) mesh.scale.set(scale, scale, scale); });
        const flashColor = new THREE.Color(0xffffff);
        finalColor.lerp(flashColor, pulseSine * 0.8);
        if (pulseProgress >= 1.0) {
          isPulsing = false;
          heartMeshes.forEach(mesh => { if (mesh) mesh.scale.set(1, 1, 1); });
        }
      }

      if (!useCustomColor || isPulsing || !initialColorApplied) {
        const r = finalColor.r, g = finalColor.g, b = finalColor.b;
        function updateParticleColorArray(attributeArray) {
          if (!attributeArray) return;
          for (let i = 0; i < attributeArray.length; i += 3) {
            attributeArray[i] = r;
            attributeArray[i + 1] = g;
            attributeArray[i + 2] = b;
          }
        }
        updateParticleColorArray(planeGeo.attributes.color.array);
        updateParticleColorArray(staticGeo.attributes.color.array);
        updateParticleColorArray(bottomGeo.attributes.color.array);
        if (staticBottomHeart) updateParticleColorArray(staticBottomHeart.geometry.attributes.color.array);
        if (staticTopHeart) updateParticleColorArray(staticTopHeart.geometry.attributes.color.array);
        updateParticleColorArray(vortexGeo.attributes.color.array);
        updateParticleColorArray(streamGeo.attributes.color.array);
        planeGeo.attributes.color.needsUpdate = true;
        staticGeo.attributes.color.needsUpdate = true;
        bottomGeo.attributes.color.needsUpdate = true;
        if (staticBottomHeart) staticBottomHeart.geometry.attributes.color.needsUpdate = true;
        if (staticTopHeart) staticTopHeart.geometry.attributes.color.needsUpdate = true;
        vortexGeo.attributes.color.needsUpdate = true;
        streamGeo.attributes.color.needsUpdate = true;
        ribbon.children.forEach(child => {
          child.material.color.setRGB(r, g, b);
        });
        initialColorApplied = true;
      }

      if (elapsedTime >= nextShootTime) {
        for (let i = 0; i < SHOOT_MAX; i++) {
          if (shootLife[i] <= 0) {
            const posIdx = 3 * i;
            const SPAWN_RADIUS = 200;
            const startPos = new THREE.Vector3(
              (Math.random() - 0.5) * 2,
              (Math.random() - 0.5) * 2,
              (Math.random() - 0.5) * 2
            ).normalize().multiplyScalar(SPAWN_RADIUS);
            shootPositions[posIdx] = startPos.x;
            shootPositions[posIdx + 1] = startPos.y;
            shootPositions[posIdx + 2] = startPos.z;
            const randomVec = new THREE.Vector3(
              (Math.random() - 0.5),
              (Math.random() - 0.5),
              (Math.random() - 0.5)
            ).normalize();
            const tangentVec = new THREE.Vector3().crossVectors(startPos, randomVec).normalize();
            const speed = 40 + 30 * Math.random();
            shootVel[posIdx] = tangentVec.x * speed;
            shootVel[posIdx + 1] = tangentVec.y * speed;
            shootVel[posIdx + 2] = tangentVec.z * speed;
            shootBirth[i] = elapsedTime;
            shootLife[i] = (SHOOT_RADIUS - SHOOT_SPAWN_RADIUS) / speed;
            shootAlpha[i] = .8 + .2 * Math.random();
            break;
          }
        }
        nextShootTime = elapsedTime + 0.5 + Math.random();
      }

      for (let i = 0; i < SHOOT_MAX; i++) {
        if (shootLife[i] > 0) {
          const posIdx = 3 * i;
          shootPositions[posIdx] += shootVel[posIdx] * delta;
          shootPositions[posIdx + 1] += shootVel[posIdx + 1] * delta;
          shootPositions[posIdx + 2] += shootVel[posIdx + 2] * delta;
          const distance = Math.hypot(shootPositions[posIdx], shootPositions[posIdx + 1], shootPositions[posIdx + 2]);
          if (distance > SHOOT_OUT_RADIUS) {
            shootLife[i] = 0;
            shootAlpha[i] = 0;
          } else {
            const threshold = .9;
            const normalizedDist = distance / SHOOT_RADIUS;
            shootAlpha[i] = normalizedDist > threshold ? 1 - (normalizedDist - threshold) / (1 - threshold) : 1;
          }
          const tailStartIdx = i * (TAIL_SEGMENTS + 1);
          const tailStartPosIdx = 3 * tailStartIdx;
          tailPositions[tailStartPosIdx] = shootPositions[posIdx];
          tailPositions[tailStartPosIdx + 1] = shootPositions[posIdx + 1];
          tailPositions[tailStartPosIdx + 2] = shootPositions[posIdx + 2];
          tailAlphas[tailStartIdx] = shootAlpha[i];
          for (let j = 1; j <= TAIL_SEGMENTS; j++) {
            const tailIdx = i * (TAIL_SEGMENTS + 1) + j;
            const tailPosIdx = 3 * tailIdx;
            tailPositions[tailPosIdx] = shootPositions[posIdx] - shootVel[posIdx] * j * TAIL_SPACING;
            tailPositions[tailPosIdx + 1] = shootPositions[posIdx + 1] - shootVel[posIdx + 1] * j * TAIL_SPACING;
            tailPositions[tailPosIdx + 2] = shootPositions[posIdx + 2] - shootVel[posIdx + 2] * j * TAIL_SPACING;
            const alpha = 1 - j / TAIL_SEGMENTS;
            tailAlphas[tailIdx] = shootAlpha[i] * alpha;
          }
        }
      }

      tailGeo.attributes.position.needsUpdate = true;
      tailGeo.attributes.alpha.needsUpdate = true;

      if (heartbeatEnabled) {
        const pulse = 1 + .05 * Math.sin(.5 * elapsedTime * Math.PI * 2);
        if (staticHeart) staticHeart.scale.set(pulse, pulse, pulse);
        if (bottomHeart) bottomHeart.scale.set(pulse, pulse, pulse);
        if (staticBottomHeart) staticBottomHeart.scale.set(pulse, pulse, pulse);
        if (staticTopHeart) staticTopHeart.scale.set(pulse, pulse, pulse);
      }

      if (revealStart !== null) {
        fadeObjects.forEach(obj => {
          if (!obj || obj === ribbon) return;
          const stage = obj.userData.fadeStage ?? 0;
          const t = THREE.MathUtils.clamp((elapsedTime - revealStart - STAGE_DURATION * stage) / STAGE_DURATION, 0, 1);
          const easeInOut = t * t * (3 - 2 * t);
          obj.traverse?.(child => {
            const material = child.material;
            if (!material) return;
            if (child.isSprite && child.userData.text && child.userData.active === false) {
              material.opacity = 0;
              return;
            }
            const baseOpacity = child.userData.baseOpacity ?? 1;
            material.opacity = baseOpacity * easeInOut;
          });
          if (stage === STAGE.STREAM && easeInOut > .1) {
            streamHeartStarted = true;
            streamHeartActiveRatio = easeInOut;
          }
        });
        if (elapsedTime - revealStart > STAGE_DURATION * (STAGE.HEART + 1)) {
          revealStart = null;
        }
      }

      if (cameraAnimationStart !== null) {
        const t = elapsedTime - cameraAnimationStart;
        const normalizedTime = THREE.MathUtils.clamp(t / CAMERA_ANIMATION_DURATION, 0, 1);
        const easeInOut = normalizedTime * normalizedTime * (3 - 2 * normalizedTime);
        camera.position.x = THREE.MathUtils.lerp(CAMERA_START_POSITION.x, CAMERA_END_POSITION.x, easeInOut);
        camera.position.y = THREE.MathUtils.lerp(CAMERA_START_POSITION.y, CAMERA_END_POSITION.y, easeInOut);
        camera.position.z = THREE.MathUtils.lerp(CAMERA_START_POSITION.z, CAMERA_END_POSITION.z, easeInOut);
        camera.lookAt(0, 0, 0);
        if (normalizedTime >= 1) {
          cameraAnimationStart = null;
          camera.position.set(CAMERA_END_POSITION.x, CAMERA_END_POSITION.y, CAMERA_END_POSITION.z);
          camera.lookAt(0, 0, 0);
        }
      }
    }

    function triggerCosmicRipple() {
      const pulseColor = new THREE.Color().setHSL((clock.getElapsedTime() * 0.05) % 1, 0.9, 0.7);
      const wave = effectPool.waves.find(w => !w.userData.active);
      if (wave) {
        wave.userData.active = true;
        wave.visible = true;
        wave.userData.creationTime = clock.getElapsedTime();
        wave.position.copy(HEART_CENTER_TARGET);
        wave.rotation.z = Math.PI;
        wave.scale.set(1, 1, 1);
        wave.material.color.copy(pulseColor);
      }
      const sparkles = effectPool.sparkles.find(s => !s.userData.active);
      if (sparkles) {
        sparkles.userData.active = true;
        sparkles.visible = true;
        sparkles.userData.creationTime = clock.getElapsedTime();
        sparkles.position.copy(HEART_CENTER_TARGET);
        sparkles.rotation.z = Math.PI;
        sparkles.material.color.copy(pulseColor);
        const positions = sparkles.geometry.attributes.position.array;
        for (let i = 0; i < 100; i++) {
          const angle = Math.random() * Math.PI * 2;
          const radius = 9;
          const speed = Math.random() * 20 + 20;
          const idx = i * 3;
          positions[idx] = Math.cos(angle) * radius;
          positions[idx + 1] = Math.sin(angle) * radius;
          positions[idx + 2] = (Math.random() - 0.5) * 5;
          if (!sparkles.userData.velocities) sparkles.userData.velocities = [];
          sparkles.userData.velocities[idx] = Math.cos(angle) * speed;
          sparkles.userData.velocities[idx + 1] = Math.sin(angle) * speed;
          sparkles.userData.velocities[idx + 2] = (Math.random() - 0.5) * 5;
        }
        sparkles.geometry.attributes.position.needsUpdate = true;
      }
    }

    setupEffectPools();

    window.addEventListener("resize", () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    const refinedBottomPos = [],
      refinedBottomColors = [],
      refinedBottomSizes = [];
    for (let i = 0; i < bottomPositions.length; i += 3) {
      const x = bottomPositions[i];
      const y = bottomPositions[i + 1];
      const z = bottomPositions[i + 2];
      if (calculateMinDistanceToBorder(x, y) < BORDER_THRESHOLD || Math.random() < .9) {
        refinedBottomPos.push(x, y, z);
        refinedBottomColors.push(heartInitialColor.r, heartInitialColor.g, heartInitialColor.b);
        refinedBottomSizes.push(bottomSizes[i / 3]);
      }
    }
    bottomPositions = refinedBottomPos;
    bottomColors.length = 0;
    bottomColors.push(...refinedBottomColors);
    bottomSizes.length = 0;
    bottomSizes.push(...refinedBottomSizes);

    const starLayers = [];

    function createStarLayer({ count, radius, colors, minSize, maxSize, opacity = 1.2 }) {
      const positions = new Float32Array(count * 3);
      const colorsAttr = new Float32Array(count * 3);
      const sizes = new Float32Array(count);
      const alpha = new Float32Array(count);
      const phase = new Float32Array(count);
      const twinkleSpeed = new Float32Array(count);
      for (let i = 0; i < count; i++) {
        const i3 = i * 3;
        const phi = Math.acos((2 * Math.random()) - 1);
        const theta = Math.random() * Math.PI * 2;
        positions[i3] = radius * Math.cos(theta) * Math.sin(phi);
        positions[i3 + 1] = radius * Math.sin(theta) * Math.sin(phi);
        positions[i3 + 2] = radius * Math.cos(phi);
        const color = colors[Math.floor(Math.random() * colors.length)];
        colorsAttr[i3] = color.r;
        colorsAttr[i3 + 1] = color.g;
        colorsAttr[i3 + 2] = color.b;
        sizes[i] = Math.random() * (maxSize - minSize) + minSize;
        alpha[i] = 1;
        phase[i] = Math.random() * Math.PI * 2;
        twinkleSpeed[i] = 0.5 + Math.random() * 1.5;
      }
      const geo = new THREE.BufferGeometry();
      geo.setAttribute('position', new THREE.BufferAttribute(positions, 3));
      geo.setAttribute('color', new THREE.BufferAttribute(colorsAttr, 3));
      geo.setAttribute('size', new THREE.BufferAttribute(sizes, 1));
      geo.setAttribute('alpha', new THREE.BufferAttribute(alpha, 1).setUsage(THREE.DynamicDrawUsage));
      geo.userData.phase = phase;
      geo.userData.twinkleSpeed = twinkleSpeed;
      const mat = makeMat({
        map: circleTexture,
        blending: THREE.AdditiveBlending,
        depthWrite: false,
        alphaSupport: true,
        opacity: opacity,
        sizeAttenuation: false,
        vertexColors: true
      });
      mat.onBeforeCompile = function (shader) {
        shader.vertexShader = shader.vertexShader.replace("uniform float pointSize;", "attribute float pointSize; varying float vAlpha; attribute float alpha;");
        shader.vertexShader = shader.vertexShader.replace("#include <project_vertex>", "#include <project_vertex> vAlpha = alpha;");
        shader.fragmentShader = shader.fragmentShader.replace("void main() {", "varying float vAlpha; void main(){");
        shader.fragmentShader = shader.fragmentShader.replace("gl_FragColor = vec4( outgoingLight, diffuseColor.a );", "gl_FragColor = vec4( outgoingLight, diffuseColor.a * vAlpha );");
      };
      return new THREE.Points(geo, mat);
    }

    const starColors = [
      new THREE.Color(0xffffff),
      new THREE.Color(0xaadcff),
      new THREE.Color(0xffffe0),
      new THREE.Color(0xffd8b1)
    ];

    const farStars = createStarLayer({
      count: 6000,
      radius: 250,
      colors: [new THREE.Color(0xaadcff), new THREE.Color(0xffffff)],
      minSize: 0.5,
      maxSize: 1.5,
      opacity: 0.8
    });

    const midStars = createStarLayer({
      count: 3000,
      radius: 180,
      colors: starColors,
      minSize: 1.0,
      maxSize: 2.5,
      opacity: 1.0
    });

    const nearStars = createStarLayer({
      count: 1000,
      radius: 120,
      colors: starColors,
      minSize: 1.5,
      maxSize: 4.0,
      opacity: 1.2
    });

    starLayers.push(farStars, midStars, nearStars);
    starLayers.forEach(layer => {
      scene.add(layer);
      layer.visible = false;
      fadeObjects.push(layer);
      layer.userData.fadeStage = STAGE.STAR;
    });

    const dustParticlesCount = 15000;
    const dustPositions = new Float32Array(dustParticlesCount * 3);
    const dustColors = new Float32Array(dustParticlesCount * 3);
    const dustColor = new THREE.Color(0x4a148c);
    for (let i = 0; i < dustParticlesCount; i++) {
      const i3 = i * 3;
      const phi = Math.acos((2 * Math.random()) - 1);
      const theta = Math.random() * Math.PI * 2;
      const radius = Math.random() * 200 + 50;
      dustPositions[i3] = radius * Math.cos(theta) * Math.sin(phi);
      dustPositions[i3 + 1] = radius * Math.sin(theta) * Math.sin(phi);
      dustPositions[i3 + 2] = radius * Math.cos(phi);
      const colorVariation = Math.random() * 0.5 + 0.5;
      dustColors[i3] = dustColor.r * colorVariation;
      dustColors[i3 + 1] = dustColor.g * colorVariation;
      dustColors[i3 + 2] = dustColor.b * colorVariation;
    }
    const dustGeometry = new THREE.BufferGeometry();
    dustGeometry.setAttribute('position', new THREE.BufferAttribute(dustPositions, 3));
    dustGeometry.setAttribute('color', new THREE.BufferAttribute(dustColors, 3));
    const dustMaterial = new THREE.PointsMaterial({
      size: 0.2,
      vertexColors: true,
      blending: THREE.AdditiveBlending,
      transparent: true,
      opacity: 0.7
    });
    const cosmicDust = new THREE.Points(dustGeometry, dustMaterial);
    scene.add(cosmicDust);

    STAR_COUNT = 0;
    starAlpha = null;
    starPhase = null;
    starGeo = null;

    const SHOOT_MAX = 10,
      TAIL_SEGMENTS = 260,
      TAIL_SPACING = .001,
      SHOOT_RADIUS = 350,
      SHOOT_POINTS = SHOOT_MAX * (1 + TAIL_SEGMENTS),
      shootPositions = new Float32Array(3 * SHOOT_MAX),
      shootVel = new Float32Array(3 * SHOOT_MAX),
      shootBirth = new Float32Array(SHOOT_MAX),
      shootLife = new Float32Array(SHOOT_MAX).fill(0),
      shootAlpha = new Float32Array(SHOOT_MAX).fill(0),
      shootSize = new Float32Array(SHOOT_MAX);
    for (let i = 0; i < SHOOT_MAX; i++) shootSize[i] = 3;

    const tailPositions = new Float32Array(3 * SHOOT_POINTS),
      tailColors = new Float32Array(3 * SHOOT_POINTS),
      tailSizes = new Float32Array(SHOOT_POINTS),
      tailAlphas = new Float32Array(SHOOT_POINTS).fill(0);
    for (let i = 0; i < SHOOT_MAX; i++) {
      tailSizes[i * (TAIL_SEGMENTS + 1)] = 6;
      for (let j = 1; j <= TAIL_SEGMENTS; j++) {
        const idx = i * (TAIL_SEGMENTS + 1) + j;
        const t = 1 - j / TAIL_SEGMENTS;
        tailSizes[idx] = 4 * t;
        const colorIdx = 3 * idx;
        tailColors[colorIdx] = .7 * t;
        tailColors[colorIdx + 1] = .8 * t;
        tailColors[colorIdx + 2] = 1 * t;
      }
    }
    for (let i = 0; i < SHOOT_MAX; i++) {
      const colorIdx = i * (TAIL_SEGMENTS + 1) * 3;
      tailColors[colorIdx] = 1;
      tailColors[colorIdx + 1] = 1;
      tailColors[colorIdx + 2] = 1;
    }

    const tailGeo = new THREE.BufferGeometry();
    tailGeo.setAttribute("position", new THREE.BufferAttribute(tailPositions, 3).setUsage(THREE.DynamicDrawUsage));
    tailGeo.setAttribute("color", new THREE.BufferAttribute(tailColors, 3));
    tailGeo.setAttribute("size", new THREE.BufferAttribute(tailSizes, 1));
    tailGeo.setAttribute("alpha", new THREE.BufferAttribute(tailAlphas, 1).setUsage(THREE.DynamicDrawUsage));

    const tailMat = makeMat({
      map: circleTexture,
      blending: THREE.AdditiveBlending,
      depthWrite: false,
      alphaSupport: true,
      vertexColors: true,
      opacity: 2,
      sizeAttenuation: false
    });
    tailMat.onBeforeCompile = function (shader) {
      shader.vertexShader = shader.vertexShader.replace("uniform float pointSize;", "attribute float pointSize; varying float vAlpha; attribute float alpha;");
      shader.vertexShader = shader.vertexShader.replace("#include <project_vertex>", "#include <project_vertex> vAlpha = alpha;");
      shader.fragmentShader = shader.fragmentShader.replace("void main() {", "varying float vAlpha; void main(){");
      shader.fragmentShader = shader.fragmentShader.replace("gl_FragColor = vec4( outgoingLight, diffuseColor.a );", "gl_FragColor = vec4( outgoingLight, diffuseColor.a * vAlpha );");
    };

    const shootingStars = new THREE.Points(tailGeo, tailMat);
    scene.add(shootingStars);
    shootingStars.userData.fadeStage = STAGE.SHOOT;

    let nextShootTime = 0;

    function triggerSceneActivation() {
      if (!heartbeatEnabled) {
        heartbeatEnabled = true;
        setupImageObjectPool();
        lastImageSpawnTime = 0;
        imageSpawnQueue.length = 0;
        currentImageIndex = 0;
        lastStatusLogTime = 0;
        nextIndependentSpawnTime = 0;
        independentImageSprites.forEach(sprite => {
          if (sprite && sprite.parent) sprite.parent.remove(sprite);
        });
        independentImageSprites.length = 0;
        fadeObjects.forEach(obj => {
          if (obj) {
            obj.visible = true;
            obj.traverse?.(child => {
              const material = child.material;
              if (material && child.userData.baseOpacity === undefined) {
                child.userData.baseOpacity = material.opacity ?? 1;
              }
              if (material) material.opacity = 0;
            });
          }
        });
        revealStart = clock.getElapsedTime();
        cameraAnimationStart = clock.getElapsedTime();
        if (userHasMovedCamera) {
          CAMERA_START_POSITION = {
            x: camera.position.x,
            y: camera.position.y,
            z: camera.position.z
          };
        }
      }
    }

    fadeObjects.push(streamHeart, shootingStars);
    [streamHeart, shootingStars].forEach(obj => {
      if (obj) {
        obj.visible = false;
        obj.traverse?.(child => {
          if (child.material && child.userData.baseOpacity === undefined) {
            child.userData.baseOpacity = child.material.opacity ?? 1;
          }
        });
      }
    });

    renderer.domElement.addEventListener("pointerdown", (event) => {
      createHeartExplosion(event);
    });

    triggerSceneActivation();

    let lastTouchEnd = 0;
    document.addEventListener("touchend", function (event) {
      const now = (new Date()).getTime();
      if (now - lastTouchEnd <= 300) {
        event.preventDefault();
      }
      lastTouchEnd = now;
    }, false);

    document.addEventListener("gesturestart", function (event) {
      event.preventDefault();
    }, { passive: false });

    document.addEventListener("gesturechange", function (event) {
      event.preventDefault();
    }, { passive: false });

    document.addEventListener("gestureend", function (event) {
      event.preventDefault();
    }, { passive: false });

    mainAnimationLoop();

    scene.add(staticBottomHeart);
    [staticTopHeart].forEach(obj => {
      if (obj) {
        obj.visible = false;
        obj.userData.fadeStage = STAGE.HEART;
        fadeObjects.push(obj);
      }
    });

    controls.addEventListener("change", () => {
      if (!userHasMovedCamera) {
        CAMERA_START_POSITION = {
          x: camera.position.x,
          y: camera.position.y,
          z: camera.position.z
        };
        userHasMovedCamera = true;
      }
    });
  </script>

  <!-- Script de Controles (Fullscreen y Música) -->
  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const fullscreenManager = {
        toggleBtn: document.getElementById('toggle-fullscreen'),
        iconElement: document.getElementById('fullscreen-icon'),
        isFullscreen: function() {
          return !!(document.fullscreenElement || document.webkitFullscreenElement || document.mozFullScreenElement || document.msFullscreenElement);
        },
        updateIcon: function() {
          if (!this.iconElement) return;
          if (this.isFullscreen()) {
            this.iconElement.classList.remove('fa-expand');
            this.iconElement.classList.add('fa-compress');
          } else {
            this.iconElement.classList.remove('fa-compress');
            this.iconElement.classList.add('fa-expand');
          }
        },
        toggle: function() {
          if (!this.isFullscreen()) {
            const element = document.documentElement;
            if (element.requestFullscreen) {
              element.requestFullscreen();
            } else if (element.mozRequestFullScreen) {
              element.mozRequestFullScreen();
            } else if (element.webkitRequestFullscreen) {
              element.webkitRequestFullscreen();
            } else if (element.msRequestFullscreen) {
              element.msRequestFullscreen();
            }
          } else {
            if (document.exitFullscreen) {
              document.exitFullscreen();
            } else if (document.mozCancelFullScreen) {
              document.mozCancelFullScreen();
            } else if (document.webkitExitFullscreen) {
              document.webkitExitFullscreen();
            } else if (document.msExitFullscreen) {
              document.msExitFullscreen();
            }
          }
        },
        init: function() {
          if (this.toggleBtn) {
            this.toggleBtn.addEventListener('click', () => this.toggle());
            document.addEventListener('fullscreenchange', () => this.updateIcon());
            document.addEventListener('webkitfullscreenchange', () => this.updateIcon());
            document.addEventListener('mozfullscreenchange', () => this.updateIcon());
            document.addEventListener('MSFullscreenChange', () => this.updateIcon());
          }
        }
      };
      fullscreenManager.init();
    });

    function setupMusicControls() {
      const music = document.getElementById("backgroundMusic");
      const musicBtn = document.getElementById("musicBtn");
      const playIcon = document.getElementById("playIcon");
      const pauseIcon = document.getElementById("pauseIcon");
      const volumeSlider = document.getElementById("volumeSlider");
      const volumeControl = document.getElementById("volumeControl");

      if (!music || !musicBtn || !volumeSlider || !volumeControl) {
        console.error('Music or control elements not found');
        return;
      }

      music.volume = volumeSlider.value;
      music.load();
      music.currentTime = 0;

      music.play().then(() => {
        console.log('Autoplay successful');
        playIcon.style.display = 'none';
        pauseIcon.style.display = 'block';
      }).catch(error => {
        console.warn('Autoplay blocked:', error.message);
      });

      function toggleMusic() {
        if (music.paused) {
          music.play().then(() => {
            console.log('Music playing');
            playIcon.style.display = 'none';
            pauseIcon.style.display = 'block';
          }).catch(error => {
            console.error('Error playing audio:', error.message);
          });
        } else {
          music.pause();
          console.log('Music paused');
          playIcon.style.display = 'block';
          pauseIcon.style.display = 'none';
        }
      }

      musicBtn.addEventListener('click', (e) => {
        e.stopPropagation();
        toggleMusic();
        if (!volumeControl.classList.contains('visible')) {
          volumeControl.classList.add('visible');
          clearTimeout(hideVolumeTimeout);
          hideVolumeTimeout = setTimeout(() => volumeControl.classList.remove('visible'), 2000);
        } else {
          volumeControl.classList.remove('visible');
        }
      });

      let hideVolumeTimeout = null;

      volumeSlider.addEventListener('input', (e) => {
        music.volume = e.target.value;
        console.log('Volume set to:', music.volume);
        clearTimeout(hideVolumeTimeout);
        volumeControl.classList.add('visible');
      });

      volumeSlider.addEventListener('change', () => {
        hideVolumeTimeout = setTimeout(() => volumeControl.classList.remove('visible'), 2000);
      });

      volumeControl.addEventListener('mouseenter', () => clearTimeout(hideVolumeTimeout));
      volumeControl.addEventListener('mouseleave', () => {
        hideVolumeTimeout = setTimeout(() => volumeControl.classList.remove('visible'), 2000);
      });

      volumeSlider.addEventListener('touchstart', (e) => {
        e.stopPropagation();
        clearTimeout(hideVolumeTimeout);
      });

      volumeSlider.addEventListener('touchend', () => {
        hideVolumeTimeout = setTimeout(() => volumeControl.classList.remove('visible'), 2000);
      });

      document.addEventListener('click', (e) => {
        if (!volumeControl.contains(e.target) && !musicBtn.contains(e.target)) {
          volumeControl.classList.remove('visible');
          clearTimeout(hideVolumeTimeout);
        }
      });

      music.addEventListener('loadeddata', () => console.log('Audio data loaded'));
      music.addEventListener('error', (e) => console.error('Audio error:', e.message));
      music.addEventListener('play', () => console.log('Music play event'));
      music.addEventListener('pause', () => console.log('Music pause event'));
    }

    setupMusicControls();
  </script>
</body>
</html>
