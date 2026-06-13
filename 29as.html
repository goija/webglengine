<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VORTEX // GLSL Torus-Engine & 29° Manifold</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body {
            background-color: #050505;
            color: #38bdf8;
            font-family: 'Monaco', 'Consolas', 'Ubuntu Mono', monospace;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        #glcanvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 1;
        }
        #overlay {
            position: absolute;
            top: 20px;
            left: 20px;
            z-index: 2;
            background: rgba(10, 15, 20, 0.85);
            padding: 15px 20px;
            border: 1px solid #1e293b;
            border-radius: 8px;
            pointer-events: none; /* Laat muisklikken door naar het canvas */
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
            backdrop-filter: blur(4px);
        }
        h1 { font-size: 1.2rem; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 5px; }
        p { font-size: 0.8rem; color: #64748b; line-height: 1.4; }
        .data-stream { color: #00FF00; margin-top: 10px; font-size: 0.75rem; }
    </style>
</head>
<body>

    <canvas id="glcanvas"></canvas>

    <div id="overlay">
        <h1>VORTEX // WebGL Engine</h1>
        <p>18x13 Faseruimte | Torus Topologie<br>
        29° Asymmetrische Torsie ($\tau$)</p>
        <div class="data-stream" id="telemetry">> INIT: u_time sync...</div>
    </div>

<script>
const canvas = document.getElementById('glcanvas');
const gl = canvas.getContext('webgl2');

if (!gl) {
    alert('WebGL2 wordt niet ondersteund in deze browser.');
}

// Pas canvas aan naar de volledige venstergrootte
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

// --- VERTEX SHADER (Basis Passthrough) ---
const vsSource = `#version 300 es
    in vec4 aVertexPosition;
    void main() {
        gl_Position = aVertexPosition;
    }
`;

// --- FRAGMENT SHADER (De VORTEX Engine met uitbreidingen) ---
const fsSource = `#version 300 es
    precision highp float;

    uniform vec2 u_resolution;
    uniform float u_time;
    uniform vec2 u_mouse; // Observer interactie
    
    out vec4 fragColor;

    #define PI 3.14159265359
    #define VORTEX_ANGLE_RAD 0.506145 // 29 graden WTC-as

    // Wuxing Ijkveld
    vec3 getWuxingColor(int element) {
        if(element == 0) return vec3(0.18, 0.54, 0.34); // Hout
        if(element == 1) return vec3(1.00, 0.27, 0.00); // Vuur
        if(element == 2) return vec3(0.85, 0.64, 0.12); // Aarde
        if(element == 3) return vec3(0.82, 0.82, 0.82); // Metaal
        return vec3(0.11, 0.56, 1.00);                  // Water
    }

    void main() {
        // Normaliseer coördinaten
        vec2 uv = gl_FragCoord.xy / u_resolution.xy;
        
        // Inverteer Y-as voor de muis, zodat het overeenkomt met de schermcoördinaten
        vec2 mouseUV = vec2(u_mouse.x, u_resolution.y - u_mouse.y) / u_resolution.xy;

        // Observer Effect: De nabijheid van de muis beïnvloedt subtiel de rotatiehoek (ruimtetijd vervorming)
        float dynamicVortex = VORTEX_ANGLE_RAD + (mouseUV.x - 0.5) * 0.1;

        // Rotatiematrix
        mat2 vortexRot = mat2(cos(dynamicVortex), -sin(dynamicVortex),
                              sin(dynamicVortex),  cos(dynamicVortex));

        // 18x13 Raster
        vec2 gridUV = vortexRot * (uv * vec2(18.0, 13.0));

        // Torus Topologie met organische oscillatie (Zandloper-golf)
        gridUV += vec2(sin(u_time * 0.5 + gridUV.y), cos(u_time * 0.3 + gridUV.x)) * 0.05;
        
        vec2 cellUV = fract(gridUV);
        vec2 cellIndex = floor(gridUV);

        // Bepaal element
        int element = int(mod(cellIndex.x * 7.0 + cellIndex.y * 3.0, 5.0));
        vec3 baseColor = getWuxingColor(element);

        // Muis/Waarnemer frictie
        float distToMouse = length(uv - mouseUV);
        float observerPressure = smoothstep(0.15, 0.0, distToMouse) * 2.0;

        // Lokale Torsie
        float torsionX = sin(u_time * 2.0 + cellIndex.x * 0.8);
        float torsionY = cos(u_time * 1.5 + cellIndex.y * 1.2);
        
        // Torsie piekt wanneer golven overlappen, of wanneer de waarnemer ingrijpt
        float torsion = torsionX * torsionY + observerPressure; 

        // Ke-frictie activatie (rode gloed)
        float frictionPulse = smoothstep(0.4, 0.9, abs(torsion));
        vec3 keHighlight = vec3(1.0, 0.1, 0.0) * frictionPulse;

        // Voronoi cel-gloed
        float edgeDist = length(cellUV - vec2(0.5));
        float nodeGlow = smoothstep(0.5, 0.1, edgeDist);

        // Samenvoegen van de structuren
        vec3 finalColor = mix(baseColor * nodeGlow, keHighlight, frictionPulse * 0.7);

        // Reizende Gray-code fotonen over het raster
        float sparkSpeed = u_time * 4.0;
        float sparkX = smoothstep(0.95, 1.0, sin(sparkSpeed + cellIndex.x));
        float sparkY = smoothstep(0.95, 1.0, cos(sparkSpeed + cellIndex.y));
        float dataSpark = max(sparkX, sparkY);
        
        // Groene injectie op de pieken
        finalColor += vec3(0.0, 1.0, 0.2) * dataSpark * 0.6;

        fragColor = vec4(finalColor, 1.0);
    }
`;

// --- Shader Compiler Functies ---
function loadShader(gl, type, source) {
    const shader = gl.createShader(type);
    gl.shaderSource(shader, source);
    gl.compileShader(shader);
    if (!gl.getShaderParameter(shader, gl.COMPILE_STATUS)) {
        console.error('Shader compile error:', gl.getShaderInfoLog(shader));
        gl.deleteShader(shader);
        return null;
    }
    return shader;
}

const vertexShader = loadShader(gl, gl.VERTEX_SHADER, vsSource);
const fragmentShader = loadShader(gl, gl.FRAGMENT_SHADER, fsSource);

const shaderProgram = gl.createProgram();
gl.attachShader(shaderProgram, vertexShader);
gl.attachShader(shaderProgram, fragmentShader);
gl.linkProgram(shaderProgram);

if (!gl.getProgramParameter(shaderProgram, gl.LINK_STATUS)) {
    console.error('Shader link error:', gl.getProgramInfoLog(shaderProgram));
}

// --- Geometrie (Full Screen Quad) ---
const positions = new Float32Array([
    -1.0,  1.0,
    -1.0, -1.0,
     1.0,  1.0,
     1.0, -1.0,
]);
const positionBuffer = gl.createBuffer();
gl.bindBuffer(gl.ARRAY_BUFFER, positionBuffer);
gl.bufferData(gl.ARRAY_BUFFER, positions, gl.STATIC_DRAW);

const positionAttributeLocation = gl.getAttribLocation(shaderProgram, 'aVertexPosition');
gl.enableVertexAttribArray(positionAttributeLocation);
gl.vertexAttribPointer(positionAttributeLocation, 2, gl.FLOAT, false, 0, 0);

// --- Uniform Locaties ---
const resolutionLocation = gl.getUniformLocation(shaderProgram, 'u_resolution');
const timeLocation = gl.getUniformLocation(shaderProgram, 'u_time');
const mouseLocation = gl.getUniformLocation(shaderProgram, 'u_mouse');

gl.useProgram(shaderProgram);

// --- Event Listeners ---
let mouseX = canvas.width / 2;
let mouseY = canvas.height / 2;

window.addEventListener('resize', () => {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    gl.viewport(0, 0, canvas.width, canvas.height);
});

canvas.addEventListener('mousemove', (e) => {
    mouseX = e.clientX;
    mouseY = e.clientY;
});

// --- De Render Loop ---
const telemetryElement = document.getElementById('telemetry');
function render(now) {
    const timeSec = now * 0.001;

    gl.uniform2f(resolutionLocation, canvas.width, canvas.height);
    gl.uniform1f(timeLocation, timeSec);
    gl.uniform2f(mouseLocation, mouseX, mouseY);

    gl.drawArrays(gl.TRIANGLE_STRIP, 0, 4);
    
    // Update de HUD
    if(Math.floor(now) % 10 === 0) {
        telemetryElement.innerText = `> τ-flux: ${Math.sin(timeSec).toFixed(4)} | G-CODE active`;
    }

    requestAnimationFrame(render);
}

requestAnimationFrame(render);
</script>

</body>
</html>
