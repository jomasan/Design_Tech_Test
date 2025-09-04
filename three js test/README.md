# Introduction to Three.js

## What is Three.js?

Three.js is a popular JavaScript library that makes it easy to create and display 3D graphics in web browsers. It's built on top of WebGL (Web Graphics Library) and provides a high-level API for creating 3D scenes, animations, and interactive experiences.

## Key Features

- **Easy 3D Graphics**: Create complex 3D scenes with simple JavaScript code
- **Cross-Platform**: Works on desktop and mobile browsers
- **Rich Ecosystem**: Extensive documentation, examples, and community support
- **Performance**: Optimized for real-time rendering
- **Extensible**: Large collection of plugins and extensions

## Basic Concepts

### 1. Scene
The scene is like a container that holds all your 3D objects, lights, and cameras.

### 2. Camera
The camera determines what the user sees. It's like a virtual eye that looks at the scene.

### 3. Renderer
The renderer draws the scene from the camera's perspective onto the screen.

### 4. Objects
3D objects like cubes, spheres, and custom geometries that populate your scene.

### 5. Materials
Materials define how objects look (color, texture, shininess, etc.).

### 6. Lights
Lights illuminate the scene and make objects visible.

## Getting Started

### Prerequisites
- Basic knowledge of HTML, CSS, and JavaScript
- A modern web browser
- A text editor

### Setup

1. **Create an HTML file** (`index.html`):
```html
<!DOCTYPE html>
<html>
<head>
    <title>Three.js Tutorial</title>
    <style>
        body { margin: 0; }
        canvas { display: block; }
    </style>
</head>
<body>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="script.js"></script>
</body>
</html>
```

2. **Create a JavaScript file** (`script.js`):
```javascript
// Basic Three.js setup
let scene, camera, renderer;

function init() {
    // Create scene
    scene = new THREE.Scene();
    
    // Create camera
    camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.z = 5;
    
    // Create renderer
    renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);
    
    // Add a cube
    const geometry = new THREE.BoxGeometry();
    const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);
    
    // Animation loop
    function animate() {
        requestAnimationFrame(animate);
        
        // Rotate the cube
        cube.rotation.x += 0.01;
        cube.rotation.y += 0.01;
        
        renderer.render(scene, camera);
    }
    animate();
}

// Handle window resize
window.addEventListener('resize', onWindowResize, false);

function onWindowResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
}

// Initialize the scene
init();
```

## Basic Examples

### 1. Rotating Cube
The example above creates a green rotating cube. Key components:
- `BoxGeometry()`: Creates a cube shape
- `MeshBasicMaterial()`: Creates a simple material
- `Mesh()`: Combines geometry and material
- `requestAnimationFrame()`: Creates smooth animation loop

### 2. Adding Lights
```javascript
// Add ambient light
const ambientLight = new THREE.AmbientLight(0x404040);
scene.add(ambientLight);

// Add directional light
const directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
directionalLight.position.set(1, 1, 1);
scene.add(directionalLight);
```

### 3. Different Materials
```javascript
// Phong material (shiny)
const phongMaterial = new THREE.MeshPhongMaterial({ color: 0x00ff00 });

// Lambert material (matte)
const lambertMaterial = new THREE.MeshLambertMaterial({ color: 0x00ff00 });

// Basic material (no lighting)
const basicMaterial = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
```

## Common Geometries

### Basic Shapes
```javascript
// Cube
const cubeGeometry = new THREE.BoxGeometry(1, 1, 1);

// Sphere
const sphereGeometry = new THREE.SphereGeometry(0.5, 32, 32);

// Cylinder
const cylinderGeometry = new THREE.CylinderGeometry(0.5, 0.5, 1, 32);

// Plane
const planeGeometry = new THREE.PlaneGeometry(2, 2);

// Torus (donut)
const torusGeometry = new THREE.TorusGeometry(0.5, 0.2, 16, 100);
```

## Camera Types

### Perspective Camera (Most Common)
```javascript
const camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);
// Parameters: FOV, aspect ratio, near plane, far plane
```

### Orthographic Camera
```javascript
const camera = new THREE.OrthographicCamera(-1, 1, 1, -1, 0.1, 1000);
// Parameters: left, right, top, bottom, near, far
```

## Controls

### Orbit Controls (Mouse/Touch)
```javascript
// Add orbit controls
const controls = new THREE.OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;
controls.dampingFactor = 0.05;

// In animation loop
controls.update();
```

## Best Practices

### 1. Performance
- Dispose of unused geometries and materials
- Use object pooling for frequently created/destroyed objects
- Limit the number of draw calls

### 2. Memory Management
```javascript
// Dispose of geometry
geometry.dispose();

// Dispose of material
material.dispose();

// Remove object from scene
scene.remove(object);
```

### 3. Responsive Design
```javascript
function onWindowResize() {
    camera.aspect = window.innerWidth / window.innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(window.innerWidth, window.innerHeight);
}
```

## Advanced Topics

### 1. Textures
```javascript
const textureLoader = new THREE.TextureLoader();
const texture = textureLoader.load('texture.jpg');
const material = new THREE.MeshBasicMaterial({ map: texture });
```

### 2. Animations
```javascript
// Using GSAP for smooth animations
gsap.to(cube.position, { x: 2, duration: 2, ease: "power2.out" });
```

### 3. Post-Processing
```javascript
// Add post-processing effects
const composer = new THREE.EffectComposer(renderer);
const renderPass = new THREE.RenderPass(scene, camera);
composer.addPass(renderPass);
```

## Resources

### Official Documentation
- [Three.js Documentation](https://threejs.org/docs/)
- [Three.js Examples](https://threejs.org/examples/)

### Learning Resources
- [Three.js Fundamentals](https://threejsfundamentals.org/)
- [Three.js Journey](https://threejs-journey.com/)

### Community
- [Three.js Forum](https://discourse.threejs.org/)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/three.js)

## Next Steps

1. **Experiment**: Try modifying the basic example
2. **Add Interactivity**: Implement mouse/touch controls
3. **Load Models**: Import 3D models (GLTF, OBJ, etc.)
4. **Shaders**: Learn about custom materials and shaders
5. **Physics**: Add physics simulation with libraries like Cannon.js

## Troubleshooting

### Common Issues

1. **Black Screen**: Check if camera is positioned correctly
2. **No Lighting**: Add lights to the scene
3. **Performance Issues**: Reduce polygon count or use LOD (Level of Detail)
4. **CORS Errors**: Serve files from a local server

### Development Server
```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx http-server

# Using PHP
php -S localhost:8000
```

---

Happy coding with Three.js! 🚀
