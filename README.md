<!-- Use # for H1 (main title), renders as largest header -->
# ParticleScreenSaver
<!-- Image syntax: ![Alt text](URL) for displaying images -->
![Sample Output](https://github.com/user-attachments/assets/5992fc0b-f9ea-4bdc-a767-7321991f66df)
<!-- Paragraphs: Plain text with blank lines between them. Use * for italic, ** for bold -->
<!-- Use ## for H2 (section headers), renders as second-largest header -->
## Features
<!-- Unordered list: Use - or * followed by a space -->
- **Hologram Transitions**: Particles transition between generated shapes using smooth animations.
- **Custom Image Support**: Upload color PNG or JPEG images to create custom hologram effects, with particles mapping to image colors.
- **Post-Processing Effects**: Utilizes UnrealBloomPass for glowing, holographic visuals.
- **Water Surface**: A reflective water plane with customizable distortion and speed enhances scene depth.
- **Responsive UI**: A dynamic control panel adapts to various screen sizes, including mobile devices.
- **Interactive Settings**: Real-time adjustments for particle count, bloom effects, water properties, and more via an intuitive interface.
## Requirements
<!-- Paragraph followed by unordered list for requirements -->
To run or modify this project, ensure you have:
- A modern web browser (*e.g.*, Chrome, Firefox, Edge) with WebGL support.
- A local web server (*e.g.*, `http-server`, Live Server in VS Code) to serve `index.html` due to CORS restrictions with Three.js texture loading.
- An image editing tool (*e.g.*, Photoshop, GIMP) for creating/editing custom images (optional).
## Customizing the Particle Screen Saver
<!-- Paragraph introducing customization -->
Customize the screen saver by interacting with the settings panel in the browser or editing `index.html` for advanced modifications. Below are instructions for adding custom images and adjusting settings.
<!-- Use ### for H3 (subsection headers) -->
### Adding Custom Images
<!-- Paragraph explaining image replacement -->
You can upload your own color PNG or JPEG images to create unique hologram effects, replacing or supplementing the default procedural shapes.
#### Image Requirements
<!-- Unordered list for image specs -->
- **Format**: PNG or JPEG with color or transparency.
- **Resolution**: Recommended `1024x1024` pixels for optimal performance and quality.
- **Style**: Images with distinct color areas work best, as particles map to RGB values. Transparent areas (alpha < 128) are ignored.
- **Example**:
<img width="345" height="382" alt="default_07" src="https://github.com/user-attachments/assets/f1a1addf-c71f-43cf-85ae-10adf1fae002" />

#### Steps to Add Custom Images
<!-- Ordered list: Use 1., 2., etc. for numbered steps -->
1. **Prepare Your Image**:
   - Create or edit an image using an image editing tool.
   - Save as PNG or JPEG in the project directory or host online (*e.g.*, GitHub, Imgur).
2. **Upload via Settings Panel**:
   - Open the screen saver in a browser.
   - Click the **SETTINGS** button (bottom-right, pulsing on first load).
   - In the **Hologram Image Sets** section, click **Load Custom Set**.
   - Select one or more PNG/JPEG files.
   - The system caches the images and transitions to them every 15 seconds.
3. **Verify Upload**:
   - Check the **Current Set** text in the panel to confirm your images loaded (e.g., `Current Set: Custom (3 images)`).
   - Particles will form shapes based on the image's colored areas.
#### Notes
<!-- Unordered list for additional notes -->
- Images with clear, high-contrast colors produce the best results.
- If an image fails to load or lacks valid colored areas, the system falls back to a default procedural sphere.
- Use a local web server for local images to avoid CORS issues.
### Available Settings
<!-- Paragraph introducing settings -->
Adjust settings via the browser's settings panel or by editing `index.html`. The panel offers sliders, checkboxes, and dropdowns for real-time control. Below are key settings and their JavaScript equivalents for advanced users.
<!-- Unordered list for settings with inline code (`) and code blocks -->
- **`particleCount`** (default: `50000`):
  - Controls the number of particles.
  - Lower values (e.g., `30000`) improve performance; higher values (e.g., `100000`) increase detail.
  - UI: Adjust via **Particle Count** slider.
  - Example:
    ```javascript
    settings.particleCount = 30000;
    ```
- **`scaleFactor`** (default: `2`):
  - Scales the size of hologram shapes.
  - UI: Not directly exposed; edit in code.
  - Example:
    ```javascript
    settings.scaleFactor = 3;
    ```
- **`transitionDuration`** (default: `25.0`):
  - Duration (in seconds) for transitions between shapes.
  - UI: Adjust via **Transition Time** slider.
  - Example:
    ```javascript
    settings.transitionDuration = 15.0;
    ```
- **`bloom.strength`** (default: `0.1`):
  - Intensity of the glow effect.
  - UI: Adjust via **Glow Strength** slider.
  - Example:
    ```javascript
    settings.bloom.strength = 0.3;
    ```
- **`bloom.radius`** (default: `0.05`):
  - Spread of the glow effect.
  - UI: Adjust via **Glow Radius** slider.
  - Example:
    ```javascript
    settings.bloom.radius = 0.2;
    ```
- **`water.distortion`** (default: `0.3`):
  - Intensity of water ripples.
  - UI: Adjust via **Water Distort** slider.
  - Example:
    ```javascript
    settings.water.distortion = 0.5;
    ```
- **`water.speed`** (default: `0.25`):
  - Speed of water animation.
  - UI: Adjust via **Water Speed** slider.
  - Example:
    ```javascript
    settings.water.speed = 0.4;
    ```
- **`lightColor`** (default: `#4F42B5`):
  - Color of ambient and spot lighting.
  - UI: Adjust via **Light Color** picker.
  - Example:
    ```javascript
    settings.lightColor = '#ff5733';
    ```
- **Presets**:
  - Predefined configurations: **Emergent**, **Skyfall**, **Mindful**.
  - UI: Click preset buttons in the **Presets** section to apply.
<!-- Paragraph introducing code-based settings -->
#### Editing Settings in Code
To modify default settings, edit the `setDefaultSettings` function in `index.html`:
    ```javascript
    function setDefaultSettings() {
        settings = {
            particleCount: 30000,
            scaleFactor: 2.5,
            transitionDuration: 20.0,
            // ... other settings
        };
        pendingSettings = JSON.parse(JSON.stringify(settings));
    }
    ```
### Using the Settings Panel
<!-- Unordered list for settings panel instructions -->
- **Open**: Click the **SETTINGS** button (bottom-right, pulses on page load).
- **Adjust**: Use sliders, checkboxes, or dropdowns for real-time changes (e.g., **Camera FOV**, **Fog Near/Far**).
- **Apply**: For settings like **Particle Count** or **Water Quality**, click **Apply & Reboot Scene** to rebuild the scene.
- **Presets**: Click **Emergent**, **Skyfall**, or **Mindful** for preconfigured effects.
- **Close**: Click the **×** button to hide the panel.

<img width="1127" height="769" alt="Settings" src="https://github.com/user-attachments/assets/86d6143c-ac7d-42f3-a0a3-64997e861591" />

## Troubleshooting
<!-- Unordered list for troubleshooting tips -->
- **CORS Errors**: Serve `index.html` via a local web server (`npm install -g http-server; http-server .`) to resolve texture loading issues.
- **Image Not Displaying**: Ensure images are valid PNG/JPEG with colored areas (alpha > 128). Check the browser console for errors.
- **Performance Issues**: Reduce `particleCount` (e.g., to `30000`) or set **Render Quality** to **Performance** in the settings panel.
- **Settings Button Invisible**: The button pulses on page load; look for a subtle orange glow in the bottom-right corner.
- **Mobile Layout Issues**: The panel should auto-adjust; ensure your browser is updated.
## License
<!-- Paragraph with link to LICENSE file -->
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
## Acknowledgments
<!-- Unordered list for acknowledgments -->
- Built with [Three.js](https://threejs.org/) for rendering and post-processing.
- Inspired by holographic particle effects for OLED/WLED displays.
- Special thanks to the Three.js community for resources and examples.
<!-- Bold and emoji for emphasis -->
**Enjoy your mesmerizing particle screen saver!** ✨
