<!-- Use # for H1 (main title), renders as largest header -->
# ParticleScreenSaver

<!-- Image syntax: ![Alt text](URL) for displaying images -->
![Sample Output](https://github.com/user-attachments/assets/5992fc0b-f9ea-4bdc-a767-7321991f66df)

<!-- Paragraphs: Plain text with blank lines between them. Use * for italic, ** for bold -->
An *artistic particle screen saver* designed for **OLED/WLED displays**, featuring **procedural fractal holograms** with smooth organic transitions. Built with [Three.js](https://threejs.org/), this project creates a visually stunning particle system that transitions between shapes, including custom user-provided images.

<!-- Use ## for H2 (section headers), renders as second-largest header -->
## Features

<!-- Unordered list: Use - or * followed by a space -->
- **Dynamic Particle Transitions**: Particles move seamlessly between shapes using quadratic Bezier curves for organic animations.
- **Custom Image Support**: Replace default shapes with your own black-and-white silhouette images.
- **Post-Processing Effects**: Utilizes UnrealBloom and Bokeh passes for a glowing, holographic effect.
- **Water Surface**: A reflective water plane enhances scene depth.
- **Star Field Background**: A twinkling cosmic backdrop adds immersion.
- **Responsive Design**: Adapts to various screen sizes with smooth rendering.

## Requirements

<!-- Paragraph followed by unordered list for requirements -->
To modify this project, ensure you have:

- A modern web browser (*e.g.*, Chrome, Firefox, Edge) with WebGL support.
- A local web server (*e.g.*, `http-server`, Live Server in VS Code) to serve `index.html` due to CORS restrictions with Three.js texture loading.
- An image editing tool (*e.g.*, Photoshop, GIMP) for creating/editing black-and-white silhouette images.

## Customizing the Particle Screen Saver

<!-- Paragraph introducing customization -->
You can customize the screen saver by editing `index.html` to add your own images or adjust settings. Below are instructions for modifying images and a list of available settings.

<!-- Use ### for H3 (subsection headers) -->
### Adding Custom Images

<!-- Paragraph explaining image replacement -->
Replace default shapes (*e.g.*, Pokémon silhouettes) with your own images by editing `index.html`.

#### Image Requirements

<!-- Unordered list for image specs -->
- **Format**: PNG with a transparent or solid background.
- **Resolution**: Recommended `1024x1024` pixels for optimal performance and quality.
- **Style**: Black-and-white silhouette where white areas (RGB > 128) define the shape. Black areas are ignored.
- **Example**:


  ![Example Silhouette](https://github.com/user-attachments/assets/94d362f1-7e98-44de-bdbe-a2913c6f3fb4)

#### Steps to Add Custom Images

<!-- Ordered list: Use 1., 2., etc. for numbered steps -->
1. **Prepare Your Image**:
   - Create or edit a black-and-white silhouette using an image editing tool.
   - Ensure the image is a PNG with white areas for the shape and black/transparent areas for the background.
   - Save the image in the project directory or host it online (*e.g.*, GitHub, Imgur).

2. **Edit `index.html`**:
   - Open `index.html` in a text editor.
   - Locate the `silhouetteFiles` array (search for `const silhouetteFiles = [];`).
   - Add or replace with your image file path/URL. For example:
     <!-- Code block: Use triple backticks with language (javascript) for syntax highlighting -->
     ```javascript
     const silhouetteFiles = [
         'path/to/your/custom_image.png'
     ];
     ```
   - For local images, place them in the project directory and ensure they are served by the local web server.
   - For online images, use the full URL (*e.g.*, `https://example.com/custom_image.png`).

3. **Test Your Changes**:
   - Save `index.html` and refresh the browser (ensure the local server is running).
   - The particle system will transition to your custom shape every 25 seconds.

#### Notes

<!-- Unordered list for additional notes -->
- The particle system uses white areas (RGB > 128) to generate points. Ensure your image has clear, distinct white shapes.
- If the image fails to load or lacks valid white areas, it falls back to a default sphere shape.
- For best results, use high-contrast images with minimal noise.

### Available Settings

<!-- Paragraph introducing settings -->
You can adjust the following settings in `index.html` to customize the screen saver's behavior and appearance. Search for these variables in the JavaScript code to modify them:

<!-- Unordered list for settings with inline code (`) and code blocks -->
- **`PARTICLE_COUNT`** (default: `75000`):
  - Controls the number of particles in the system.
  - Lower values (e.g., `50000`) improve performance on lower-end devices but reduce visual density.
  - Example:
    ```javascript
    const PARTICLE_COUNT = 50000;
    ```

- **`SCALE_FACTOR`** (default: `2`):
  - Scales the size of the particle shapes.
  - Increase for larger shapes (e.g., `3`), decrease for smaller shapes (e.g., `1.5`).
  - Example:
    ```javascript
    const SCALE_FACTOR = 3;
    ```

- **`TRANSITION_DURATION`** (default: `8.0`):
  - Duration (in seconds) for particle transitions between shapes.
  - Increase for slower transitions (e.g., `12.0`), decrease for faster transitions (e.g., `5.0`).
  - Example:
    ```javascript
    const TRANSITION_DURATION = 10.0;
    ```

- **`STAR_COUNT`** (default: `1000`):
  - Number of stars in the background star field.
  - Reduce for better performance (e.g., `500`), increase for a denser star field (e.g., `2000`).
  - Example:
    ```javascript
    const STAR_COUNT = 1500;
    ```

- **Bloom Pass Settings**:
  - Located in the `UnrealBloomPass` constructor: `UnrealBloomPass(new THREE.Vector2(window.innerWidth, window.innerHeight), 0.2, 0.1, 0.2)`.
  - Adjust parameters for bloom effect intensity:
    - `strength` (default: `0.2`): Increase (e.g., `0.5`) for stronger glow, decrease (e.g., `0.1`) for subtler glow.
    - `radius` (default: `0.1`): Increase (e.g., `0.3`) for broader glow spread.
    - `threshold` (default: `0.2`): Increase (e.g., `0.4`) to limit glow to brighter areas.
    - Example:
      ```javascript
      UnrealBloomPass(new THREE.Vector2(window.innerWidth, window.innerHeight), 0.4, 0.2, 0.3);
      ```

- **Water Surface Settings**:
  - Located in the `Water` constructor and `water.material.uniforms`.
  - Adjust `distortionScale` (default: `0.3`) for water ripple intensity (e.g., `0.5` for stronger ripples).
  - Modify `waterColor` (default: `0x000000`) to change water tint (e.g., `0x1a2b3c` for a bluish hue).
  - Example:
    ```javascript
    water.material.uniforms['distortionScale'].value = 0.5;
    ```

## Troubleshooting

<!-- Unordered list for troubleshooting tips -->
- **CORS Errors**: Use a local web server to serve `index.html`, as opening it directly in the browser may cause texture loading issues.
- **Image Not Displaying**: Verify the image is a valid PNG with white silhouette areas (RGB > 128). Check the browser console for errors.
- **Performance Issues**: Reduce `PARTICLE_COUNT` (e.g., to `50000`) for lower-end devices.

## License

<!-- Paragraph with link to LICENSE file -->
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

<!-- Unordered list for acknowledgments -->
- Built with [Three.js](https://threejs.org/) for rendering and post-processing.
- Inspired by holographic and particle-based visual effects for OLED/WLED displays.

<!-- Bold and emoji for emphasis -->
**Enjoy crafting your own particle screen saver!** ✨
