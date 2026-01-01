Difficulty: 
Hey, I'm Evan! I like to build things. All sorts of things. If you aren't failing on some front, consider adjusting your difficulty settings.

So here's the deal - there are some seriously bizarre signals floating around this area.

Not your typical radio chatter or WiFi noise, but something... different.

I've been trying to make sense of the patterns, but it's like trying to build a robot hand out of a coffee maker - you need the right approach.

Think you can help me decode whatever weirdness is being transmitted out there?


https://signals.holidayhackchallenge.com/?&challenge=termSignals&username=hackadviser&id=4107cbf6-ba28-41ff-93b0-9fa2c46c201f 
## Hints

## On Rails
 
**Stage-by-stage approach**

1. Connect to the captured wire files or endpoints for the relevant wires.
2. Collect all frames for the transmission (buffer until inactivity or loop boundary).
3. Identify protocol from wire names (e.g., `dq` → 1-Wire; `mosi`/`sck` → SPI; `sda`/`scl` → I²C).
4. Decode the raw signal:
    - Pulse-width protocols: locate falling→rising transitions and measure low-pulse width.
    - Clocked protocols: detect clock edges and sample the data line at the specified sampling phase.
5. Assemble bits into bytes taking the correct bit order (LSB vs MSB).
6. Convert bytes to text (printable ASCII or hex as appropriate).
7. Extract information from the decoded output — it contains the XOR key or other hints for the next stage.

8. Repeat Stage 1 decoding to recover raw bytes (they will appear random).
9. Apply XOR decryption using the key obtained from the previous stage.
10. Inspect decrypted output for next-stage keys or target device information.

- Multiple 7-bit device addresses share the same SDA/SCL lines.
- START condition: SDA falls while SCL is high. STOP: SDA rises while SCL is high.
- First byte of a transaction = (7-bit address << 1) | R/W. Extract address with `address = first_byte >> 1`.
- Identify and decode every device’s transactions; decrypt only the target device’s payload.

- Print bytes in hex and as ASCII (if printable) — hex patterns reveal structure.
- Check printable ASCII range (0x20–0x7E) to spot valid text.
- Verify endianness: swapping LSB/MSB will quickly break readable text.
- For XOR keys, test short candidate keys and look for common English words.
- If you connect mid-broadcast, wait for the next loop or detect a reset/loop marker before decoding.

- Buffering heuristic: treat the stream complete after a short inactivity window (e.g., 500 ms) or after a full broadcast loop.
- Sort frames by timestamp per wire and collapse consecutive identical levels before decoding to align with the physical waveform.


## Protocols

---

**Key concept - Clock vs. Data signals:**

- Some protocols have separate clock and data lines (like SPI and I2C)
- For clocked protocols, you need to sample the data line at specific moments defined by the clock
- The clock signal tells you _when_ to read the data signal

**For 1-Wire (no separate clock):**

- Information is encoded in pulse widths (how long the signal stays low or high)
- Different pulse widths represent different bit values
- Look for patterns in the timing between transitions

**For SPI and I2C:**

- Identify which line is the clock (SCL for I2C, SCK for SPI)
- Data is typically valid/stable when the clock is in a specific state (high or low)
- You need to detect clock edges (transitions) and sample data at those moments

**Technical approach:**

- Sort frames by timestamp
- Detect rising edges (0→1) and falling edges (1→0) on the clock line
- Sample the data line's value at each clock edge

## Bits and Bytes


**Critical detail - Bit ordering varies by protocol:**

**MSB-first (Most Significant Bit first):**

- SPI and I2C typically send the highest bit (bit 7) first
- When assembling bytes: `byte = (byte << 1) | bit_value`
- Start with an empty byte, shift left, add the new bit

**LSB-first (Least Significant Bit first):**

- 1-Wire and UART send the lowest bit (bit 0) first
- When assembling bytes: `byte |= bit_value << bit_position`
- Build the byte from bit 0 to bit 7

**I2C specific considerations:**

- Every 9th bit is an ACK (acknowledgment) bit - ignore these when decoding data
- The first byte in each transaction is the device address (7 bits) plus a R/W bit
- You may need to filter for specific device addresses

**Converting bytes to text:**

```javascript
String.fromCharCode(byte_value)  // Converts byte to ASCII character
```


## Garbage?

**If your decoded data looks like gibberish:**

- The data may be encrypted with XOR cipher
- XOR is a simple encryption: `encrypted_byte XOR key_byte = plaintext_byte`
- The same operation both encrypts and decrypts: `plaintext XOR key = encrypted`, `encrypted XOR key = plaintext`

**How XOR cipher works:**

```javascript
function xorDecrypt(encrypted, key) {
  let result = "";
  for (let i = 0; i < encrypted.length; i++) {
    const encryptedChar = encrypted.charCodeAt(i);
    const keyChar = key.charCodeAt(i % key.length);  // Key repeats
    result += String.fromCharCode(encryptedChar ^ keyChar);
  }
  return result;
}
```

**Key characteristics:**

- The key is typically short and repeats for the length of the message
- You need the correct key to decrypt (look for keys in previous stage messages)
- If you see readable words mixed with garbage, you might have the wrong key or bit order

**Testing your decryption:**

- Encrypted data will have random-looking byte values
- Decrypted data should be readable ASCII text
- Try different keys from messages you've already decoded


## Structure

 **What you're dealing with:**

- You have access to WebSocket endpoints that stream digital signal data
- Each endpoint represents a physical wire in a hardware communication system
- The data comes as JSON frames with three properties: `line` (wire name), `t` (timestamp), and `v` (value: 0 or 1)
- The server continuously broadcasts signal data in a loop - you can connect at any time
- This is a multi-stage challenge where solving one stage reveals information needed for the next

**Where to start:**

- Connect to a WebSocket endpoint and observe the data format
- The server automatically sends data every few seconds - just wait and collect
- Look for documentation on the protocol types mentioned (1-Wire, SPI, I2C)
- Consider that hardware protocols encode information in the _timing_ and _sequence_ of signal transitions, not just the values themselves
- Consider capturing the WebSocket frames to a file so you can work offline

## Solve

### dato 1
```
https://signals.holidayhackchallenge.com/?&challenge=termSignals&username=hackadviser&id=4107cbf6-ba28-41ff-93b0-9fa2c46c201f


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hardware Protocol Challenge - Signal Monitor</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html, body {
            width: 100%;
            height: 100%;
        }

        body {
            font-family: 'Courier New', monospace;
            background: #0a0e27 url('background.png') no-repeat center center fixed;
            background-size: cover;
            color: #00ff41;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            width: 900px;
            height: 700px;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            perspective-origin: center center;
            perspective: 2180px;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
            background: rgba(0, 255, 65, 0.05);
            border: 2px solid #00ff41;
            border-radius: 8px;
        }

        h1 {
            font-size: 2rem;
            margin-bottom: 10px;
            text-shadow: 0 0 10px #00ff41;
        }

        .subtitle {
            color: #00cc33;
            font-size: 0.9rem;
        }

        /* Mobile Phone Mockup Container */
        .phone-mockup {
            width: 400px;
            margin: 0 auto;
            background: #000000;
            border-radius: 15px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            border: 8px solid #1b1710;
            position: absolute;
            transform: rotateY(-10deg) rotateZ(0deg) skewX(0deg) skewY(2deg);
            height: 412px;
            left: calc(50% - 222px);
            top: calc(50% - 150px);
            transform-style: preserve-3d;
        }

        .phone-screen {
            background: #181818;
            border-radius: 15px;
            overflow: hidden;
        }

        .phone-header {
            background: linear-gradient(135deg, #1a1e3f 0%, #0a0e27 100%);
            padding: 20px 15px;
            text-align: center;
            border-bottom: 2px solid #00ff41;
        }

        .phone-title {
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 5px;
            text-shadow: 0 0 10px #00ff41;
        }

        .phone-subtitle {
            font-size: 0.7rem;
            color: #00cc33;
            opacity: 0.8;
        }

        /* Tab Navigation */
        .tab-nav {
            display: flex;
            background: #000000;
            border-bottom: 2px solid #00ff41;
        }

        .tab-button {
            flex: 1;
            padding: 12px 8px;
            background: transparent;
            border: none;
            color: #666;
            font-family: inherit;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            border-bottom: 3px solid transparent;
        }

        .tab-button.active {
            color: #00ff41;
            border-bottom-color: #00ff41;
            background: rgba(0, 255, 65, 0.05);
        }

        .tab-button:hover:not(.active) {
            background: rgba(0, 255, 65, 0.02);
        }

        .tab-icon {
            font-size: 1.5rem;
            display: block;
            margin-bottom: 3px;
        }

        /* Tab Content */
        .tab-content {
            display: none;
            padding: 15px;
            max-height: 600px;
            overflow-y: auto;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Protocol Info */
        .protocol-info {
            background: rgba(0, 255, 65, 0.05);
            border: 1px solid #00ff41;
            border-radius: 8px;
            padding: 12px;
            margin-bottom: 15px;
            font-size: 0.75rem;
        }

        .protocol-info h3 {
            font-size: 0.85rem;
            margin-bottom: 8px;
            color: #00ffff;
        }

        .protocol-info p {
            color: #888;
            line-height: 1.4;
        }

        /* Status Badge */
        .status-badge {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 0.7rem;
            font-weight: 600;
            margin-bottom: 12px;
        }

        .status-badge.connected {
            background: rgba(0, 255, 65, 0.2);
            color: #00ff41;
            border: 1px solid #00ff41;
        }

        .status-badge.disconnected {
            background: rgba(255, 68, 68, 0.2);
            color: #ff4444;
            border: 1px solid #ff4444;
        }

        .status-dot {
            width: 6px;
            height: 6px;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        .status-badge.connected .status-dot {
            background: #00ff41;
        }

        .status-badge.disconnected .status-dot {
            background: #ff4444;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        /* Wire Cards */
        .wire-card {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 8px;
            padding: 10px;
            margin-bottom: 12px;
            border: 1px solid rgba(0, 255, 65, 0.2);
        }

        .wire-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }

        .wire-name {
            font-weight: 600;
            color: #00ffff;
            font-size: 0.8rem;
        }

        .wire-stats {
            display: flex;
            gap: 10px;
            font-size: 0.65rem;
            color: #00cc33;
        }

        .zoom-indicator {
            color: #888;
        }

        /* Signal Display */
        .signal-display {
            background: #000;
            padding: 8px;
            border-radius: 6px;
            overflow-x: auto;
            overflow-y: hidden;
            height: 70px;
            margin-bottom: 8px;
        }

        .signal-canvas {
            display: block;
            image-rendering: crisp-edges;
        }

        /* Buttons */
        .button-group {
            display: flex;
            gap: 6px;
            margin-top: 12px;
        }

        .btn {
            flex: 1;
            padding: 10px 8px;
            border: none;
            border-radius: 6px;
            font-family: inherit;
            font-size: 0.7rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            text-transform: uppercase;
        }

        .btn-primary {
            background: #00ff41;
            color: #0a0e27;
        }

        .btn-primary:active {
            transform: scale(0.95);
            background: #00cc33;
        }

        .btn-secondary {
            background: rgba(0, 255, 65, 0.1);
            color: #00ff41;
            border: 1px solid #00ff41;
        }

        .btn-secondary:active {
            transform: scale(0.95);
            background: rgba(0, 255, 65, 0.2);
        }

        /* Message Log */
        .message-log {
            background: #000;
            padding: 8px;
            border-radius: 6px;
            font-size: 0.65rem;
            max-height: 100px;
            overflow-y: auto;
            margin-top: 10px;
            font-family: 'Courier New', monospace;
        }

        .message-log div {
            margin: 3px 0;
            line-height: 1.3;
        }

        .timestamp {
            color: #666;
        }

        .gnome-holder {
            position: absolute;
            left: calc(50% - 512px);
            height: auto;
            opacity: 0.8;
            top: calc(50% - 928px);
            z-index: -1;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- <header>
            <h1>Hardware Hacking Challenge</h1>
            <div class="subtitle">WebSocket Protocol Analyzer</div>
        </header> -->

        <!-- Mobile Phone Mockup -->
        <div class="phone-mockup">
            <div class="phone-screen">
                <!-- <div class="phone-header">
                    <div class="phone-title">Protocol Analyzer</div>
                    <div class="phone-subtitle">Hardware Challenge</div>
                </div> -->

                <!-- Tab Navigation -->
                <nav class="tab-nav">
                    <button class="tab-button active" onclick="switchTab('1wire')">
                        <span>1-Wire</span>
                    </button>
                    <button class="tab-button" onclick="switchTab('spi')">
                        <span>SPI</span>
                    </button>
                    <button class="tab-button" onclick="switchTab('i2c')">
                        <span>I2C</span>
                    </button>
                </nav>

                <!-- 1-Wire Tab -->
                <div id="tab-1wire" class="tab-content active">
                    <div class="status-badge disconnected" id="status-1wire">
                        <span class="status-dot"></span>
                        <span>Disconnected</span>
                    </div>

                    <div class="wire-card">
                        <div class="wire-header">
                            <span class="wire-name">DQ (Data)</span>
                        </div>
                        <div class="signal-display" id="signal-dq">
                            <canvas id="canvas-dq" class="signal-canvas"></canvas>
                        </div>
                    </div>
                </div>

                <!-- SPI Tab -->
                <div id="tab-spi" class="tab-content">
                    <div class="status-badge disconnected" id="status-spi">
                        <span class="status-dot"></span>
                        <span>Disconnected</span>
                    </div>

                    <div class="wire-card">
                        <div class="wire-header">
                            <span class="wire-name">MOSI (Master Out)</span>
                        </div>
                        <div class="signal-display" id="signal-mosi">
                            <canvas id="canvas-mosi" class="signal-canvas"></canvas>
                        </div>
                    </div>

                    <div class="wire-card">
                        <div class="wire-header">
                            <span class="wire-name">SCK (Clock)</span>
                        </div>
                        <div class="signal-display" id="signal-sck">
                            <canvas id="canvas-sck" class="signal-canvas"></canvas>
                        </div>
                    </div>
                </div>

                <!-- I2C Tab -->
                <div id="tab-i2c" class="tab-content">
                    <div class="status-badge disconnected" id="status-i2c">
                        <span class="status-dot"></span>
                        <span>Disconnected</span>
                    </div>

                    <div class="wire-card">
                        <div class="wire-header">
                            <span class="wire-name">SDA (Data)</span>
                        </div>
                        <div class="signal-display" id="signal-sda">
                            <canvas id="canvas-sda" class="signal-canvas"></canvas>
                        </div>
                    </div>

                    <div class="wire-card">
                        <div class="wire-header">
                            <span class="wire-name">SCL (Clock)</span>
                        </div>
                        <div class="signal-display" id="signal-scl">
                            <canvas id="canvas-scl" class="signal-canvas"></canvas>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="gnome-holder">
            <img src="gnome.png" alt="Gnome" class="gnome-image">
        </div>
    </div>

    <script>
        // WebSocket connections storage
        const connections = {};
        const maxSignalBits = 500;
        const maxLogMessages = 50;

        // Signal data storage for each wire
        const signalData = {
            'dq': [],
            'mosi': [],
            'sck': [],
            'sda': [],
            'scl': []
        };

        // Zoom level for each wire (pixels per bit)
        const zoomLevels = {
            'dq': 4,
            'mosi': 4,
            'sck': 4,
            'sda': 4,
            'scl': 4
        };

        const MIN_ZOOM = 1;
        const MAX_ZOOM = 20;

        // Canvas settings
        const CANVAS_HEIGHT = 54;
        const HIGH_LEVEL = 8;
        const LOW_LEVEL = CANVAS_HEIGHT - 8;
        const LINE_COLOR = '#00ff41';
        const GLOW_COLOR = 'rgba(0, 255, 65, 0.5)';
        const GRID_COLOR = 'rgba(0, 255, 65, 0.1)';

        // Wire to protocol mapping
        const wireToProtocol = {
            'dq': '1wire',
            'mosi': 'spi',
            'sck': 'spi',
            'sda': 'i2c',
            'scl': 'i2c'
        };

        // Tab switching with auto-connect
        function switchTab(tabName) {
            // Disconnect wires from previous tab
            const previousTab = document.querySelector('.tab-content.active');
            if (previousTab) {
                const previousTabId = previousTab.id.replace('tab-', '');
                const wiresToDisconnect = getProtocolWires(previousTabId);
                wiresToDisconnect.forEach(wire => disconnectWire(wire));
            }

            // Update tab buttons
            document.querySelectorAll('.tab-button').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.closest('.tab-button').classList.add('active');

            // Update tab content
            document.querySelectorAll('.tab-content').forEach(content => {
                content.classList.remove('active');
            });
            document.getElementById(`tab-${tabName}`).classList.add('active');

            // Auto-connect wires for new tab
            const wiresToConnect = getProtocolWires(tabName);
            wiresToConnect.forEach(wire => connectWire(wire, tabName));
        }

        // Helper function to get wires for a protocol
        function getProtocolWires(protocol) {
            const protocolWires = {
                '1wire': ['dq'],
                'spi': ['mosi', 'sck'],
                'i2c': ['sda', 'scl']
            };
            return protocolWires[protocol] || [];
        }

        // Initialize canvases
        function initCanvas(wireName) {
            const canvas = document.getElementById(`canvas-${wireName}`);
            if (!canvas) return null;

            const container = canvas.parentElement;
            const width = container.clientWidth - 16;
            canvas.width = width;
            canvas.height = CANVAS_HEIGHT;
            canvas.style.width = width + 'px';
            canvas.style.height = CANVAS_HEIGHT + 'px';

            const ctx = canvas.getContext('2d');
            drawGrid(ctx, width, CANVAS_HEIGHT);
            
            return { canvas, ctx };
        }

        // Draw oscilloscope grid
        function drawGrid(ctx, width, height) {
            ctx.strokeStyle = GRID_COLOR;
            ctx.lineWidth = 1;

            for (let y = 0; y < height; y += 13) {
                ctx.beginPath();
                ctx.moveTo(0, y);
                ctx.lineTo(width, y);
                ctx.stroke();
            }

            for (let x = 0; x < width; x += 16) {
                ctx.beginPath();
                ctx.moveTo(x, 0);
                ctx.lineTo(x, height);
                ctx.stroke();
            }
        }

        // Draw waveform on canvas
        function drawWaveform(wireName) {
            const canvasInfo = initCanvas(wireName);
            if (!canvasInfo) return;

            const { canvas, ctx } = canvasInfo;
            const width = canvas.width;
            const data = signalData[wireName];
            const pixelsPerBit = zoomLevels[wireName];

            ctx.fillStyle = '#000';
            ctx.fillRect(0, 0, width, CANVAS_HEIGHT);
            drawGrid(ctx, width, CANVAS_HEIGHT);

            if (data.length === 0) return;

            const maxBitsOnScreen = Math.floor(width / pixelsPerBit);
            const startIdx = Math.max(0, data.length - maxBitsOnScreen);
            const visibleData = data.slice(startIdx);

            // Draw glow effect
            ctx.strokeStyle = GLOW_COLOR;
            ctx.lineWidth = 3;
            ctx.lineCap = 'round';
            ctx.lineJoin = 'round';
            drawSignalPath(ctx, visibleData, 0, pixelsPerBit);

            // Draw main signal line
            ctx.strokeStyle = LINE_COLOR;
            ctx.lineWidth = 2;
            ctx.lineCap = 'round';
            ctx.lineJoin = 'round';
            drawSignalPath(ctx, visibleData, 0, pixelsPerBit);

            // Draw dots at transitions
            ctx.fillStyle = LINE_COLOR;
            for (let i = 0; i < visibleData.length; i++) {
                const x = i * pixelsPerBit;
                const y = visibleData[i] === 1 ? HIGH_LEVEL : LOW_LEVEL;
                
                if (i === 0 || visibleData[i] !== visibleData[i - 1]) {
                    ctx.beginPath();
                    ctx.arc(x, y, 2, 0, Math.PI * 2);
                    ctx.fill();
                }
            }
        }

        // Draw the signal path
        function drawSignalPath(ctx, data, xOffset, pixelsPerBit) {
            if (data.length === 0) return;

            ctx.beginPath();
            
            let currentY = data[0] === 1 ? HIGH_LEVEL : LOW_LEVEL;
            ctx.moveTo(xOffset, currentY);

            for (let i = 0; i < data.length; i++) {
                const x = i * pixelsPerBit + xOffset;
                const nextY = data[i] === 1 ? HIGH_LEVEL : LOW_LEVEL;

                if (i > 0 && data[i] !== data[i - 1]) {
                    ctx.lineTo(x, currentY);
                    ctx.lineTo(x, nextY);
                } else {
                    ctx.lineTo(x, nextY);
                }

                currentY = nextY;
            }

            ctx.lineTo(data.length * pixelsPerBit + xOffset, currentY);
            ctx.stroke();
        }

        // Handle zoom via mousewheel
        function handleZoom(wireName, event) {
            event.preventDefault();
            
            const zoomDelta = event.deltaY > 0 ? -0.5 : 0.5;
            const newZoom = Math.max(MIN_ZOOM, Math.min(MAX_ZOOM, zoomLevels[wireName] + zoomDelta));
            
            if (newZoom !== zoomLevels[wireName]) {
                zoomLevels[wireName] = newZoom;
                drawWaveform(wireName);
                updateZoomIndicator(wireName);
            }
        }

        // Update zoom indicator display
        function updateZoomIndicator(wireName) {
            const indicator = document.getElementById(`zoom-${wireName}`);
            if (indicator) {
                indicator.textContent = `${zoomLevels[wireName].toFixed(1)}x`;
            }
        }

        // Attach zoom handlers to canvases
        function attachZoomHandler(wireName) {
            const canvas = document.getElementById(`canvas-${wireName}`);
            if (canvas) {
                canvas.addEventListener('wheel', (e) => handleZoom(wireName, e), { passive: false });
                canvas.style.cursor = 'zoom-in';
                canvas.title = `Scroll to zoom (${zoomLevels[wireName].toFixed(1)}x)`;
            }
        }

        // Connect to a specific wire
        function connectWire(wireName, protocolName) {
            if (connections[wireName]) {
                addLog(protocolName, `Already connected to ${wireName}`);
                return;
            }

            initCanvas(wireName);

            const proto = location.protocol === 'https:' ? 'wss' : 'ws';
            const host = location.host || location.hostname; // includes port if present in current URL
            const ws = new WebSocket(`${proto}://${host}/wire/${wireName}`);
            connections[wireName] = ws;

            ws.onopen = () => {
                updateStatus(protocolName);
                addLog(protocolName, `Connected to ${wireName}`);
            };

            ws.onmessage = (event) => {
                try {
                    const data = JSON.parse(event.data);
                    
                    if (data.type === 'welcome') {
                        addLog(protocolName, `Server: ${data.message}`);
                        return;
                    }

                    if (data.line && typeof data.v !== 'undefined') {
                        updateSignal(data.line, data.v, data.t);
                        updateFrameCount(data.line);
                    }
                } catch (e) {
                    console.error('Error parsing message:', e);
                }
            };

            ws.onerror = (error) => {
                console.error(`WebSocket error on ${wireName}:`, error);
                addLog(protocolName, `Error on ${wireName}`);
            };

            ws.onclose = () => {
                delete connections[wireName];
                updateStatus(protocolName);
                addLog(protocolName, `Disconnected from ${wireName}`);
            };
        }

        // Disconnect from a specific wire
        function disconnectWire(wireName) {
            if (connections[wireName]) {
                connections[wireName].close();
                delete connections[wireName];
                const protocol = wireToProtocol[wireName];
                updateStatus(protocol);
            }
        }

        // Connect to all wires in a protocol
        function connectProtocol(protocolName, wires) {
            wires.forEach(wire => connectWire(wire, protocolName));
        }

        // Disconnect from all wires in a protocol
        function disconnectProtocol(wires) {
            wires.forEach(wire => disconnectWire(wire));
        }

        // Update signal display with new bit
        function updateSignal(wireName, value, timestamp) {
            if (!signalData[wireName]) return;

            signalData[wireName].push(value);

            if (signalData[wireName].length > maxSignalBits) {
                signalData[wireName].shift();
            }

            drawWaveform(wireName);
        }

        // Update frame count
        function updateFrameCount(wireName) {
            const countSpan = document.getElementById(`count-${wireName}`);
            if (countSpan) {
                const current = parseInt(countSpan.textContent) || 0;
                countSpan.textContent = current + 1;
            }
        }

        // Update protocol connection status
        function updateStatus(protocolName) {
            const statusBadge = document.getElementById(`status-${protocolName}`);
            if (!statusBadge) return;

            const wires = {
                '1wire': ['dq'],
                'spi': ['mosi', 'sck'],
                'i2c': ['sda', 'scl']
            }[protocolName] || [];

            const connectedCount = wires.filter(w => connections[w]).length;
            const isConnected = connectedCount > 0;

            statusBadge.className = `status-badge ${isConnected ? 'connected' : 'disconnected'}`;
            statusBadge.innerHTML = `<span class="status-dot"></span><span>${isConnected ? `Connected (${connectedCount}/${wires.length})` : 'Disconnected'}</span>`;
        }

        // Add message to log
        function addLog(protocolName, message) {
            const logDiv = document.getElementById(`log-${protocolName}`);
            if (!logDiv) return;

            const timestamp = new Date().toLocaleTimeString();
            const logEntry = document.createElement('div');
            logEntry.innerHTML = `<span class="timestamp">[${timestamp}]</span> ${message}`;
            
            logDiv.appendChild(logEntry);

            while (logDiv.children.length > maxLogMessages) {
                logDiv.removeChild(logDiv.firstChild);
            }

            logDiv.scrollTop = logDiv.scrollHeight;
        }

        // Clear signal display
        function clearSignal(wireName) {
            if (signalData[wireName]) {
                signalData[wireName] = [];
            }
            
            initCanvas(wireName);
            
            const countSpan = document.getElementById(`count-${wireName}`);
            if (countSpan) {
                countSpan.textContent = '0';
            }
        }

        // Clear protocol signals
        function clearProtocol(wires) {
            wires.forEach(wire => clearSignal(wire));
            const protocol = wireToProtocol[wires[0]];
            const logDiv = document.getElementById(`log-${protocol}`);
            if (logDiv) {
                logDiv.innerHTML = '';
            }
        }

        // Initialize canvases on page load
        window.addEventListener('load', () => {
            ['dq', 'mosi', 'sck', 'sda', 'scl'].forEach(wire => {
                initCanvas(wire);
                attachZoomHandler(wire);
            });
            
            // Auto-connect 1-Wire on initial load
            connectWire('dq', '1wire');
        });

        // Handle window resize
        window.addEventListener('resize', () => {
            ['dq', 'mosi', 'sck', 'sda', 'scl'].forEach(wire => {
                drawWaveform(wire);
            });
        });

        // Cleanup on page unload
        window.addEventListener('beforeunload', () => {
            Object.keys(connections).forEach(wire => disconnectWire(wire));
        });
    </script>
</body>
</html>

```

### dato 2
```

```

## Solve  Inteto 1

### stage 1

solve-dq.py
```python
import json

FILENAME = 'dq_data.json'

def decode_1wire():
    try:
        with open(FILENAME, 'r') as f:
            frames = json.load(f)
    except FileNotFoundError:
        print(f"[!] Error: No se encuentra el archivo {FILENAME}")
        return

    bits = []
    last_falling_edge = 0
    
    for i in range(1, len(frames)):
        prev = frames[i-1]
        curr = frames[i]
        
        # Detectar Flanco de BAJADA (Inicio de pulso)
        if prev['v'] == 1 and curr['v'] == 0:
            last_falling_edge = curr['t']
            
        # Detectar Flanco de SUBIDA (Fin de pulso)
        elif prev['v'] == 0 and curr['v'] == 1:
            duration = curr['t'] - last_falling_edge
            
            # Reset/Presencia (ignorar)
            if duration > 400:
                continue 
            
            # Decodificación (Short=1, Long=0)
            if duration < 30:
                bits.append('1')
            else:
                bits.append('0')

    # --- CORRECCIÓN DE ALINEACIÓN ---
    # El primer bit detectado es basura (un '0' residual). Lo saltamos.
    # Esto alinea el flujo para que empiece correctamente con el comando 0xCC
    if len(bits) > 0 and bits[0] == '0':
        print("[*] Aplicando corrección de desplazamiento de bits...")
        bits = bits[1:]

    print(f"[*] Total bits útiles: {len(bits)}")
    
    message_ascii = ""
    
    # Procesar en Bytes (LSB First)
    for i in range(0, len(bits), 8):
        byte_chunk = bits[i:i+8]
        if len(byte_chunk) < 8: break
            
        # Invertir orden (LSB -> MSB para conversión)
        inverted_bits = "".join(byte_chunk[::-1])
        char_code = int(inverted_bits, 2)
        
        if 32 <= char_code <= 126:
            message_ascii += chr(char_code)
        else:
            # Solo para debug, el 0xCC inicial no es imprimible
            pass 

    print("\n--- MENSAJE DECODIFICADO ---")
    print(message_ascii)
    print("----------------------------")

if __name__ == "__main__":
    decode_1wire()
```

```bash
python solve-dq.py 
[*] Aplicando corrección de desplazamiento de bits...
[*] Total bits útiles: 456

--- MENSAJE DECODIFICADO ---
read and decrypt the SPI bus data using the XOR key: icy
```

### stage 2

solve-spy.py

```python
import json

# Archivos capturados
FILE_MOSI = 'mosi_data.json'
FILE_SCK = 'sck_data.json'

# Clave obtenida en la fase anterior (1-Wire)
XOR_KEY = "icy"

def solve_spi():
    print(f"[*] Cargando archivos {FILE_MOSI} y {FILE_SCK}...")
    try:
        with open(FILE_MOSI, 'r') as f:
            mosi_data = json.load(f)
        with open(FILE_SCK, 'r') as f:
            sck_data = json.load(f)
    except FileNotFoundError as e:
        print(f"[!] Error: {e}")
        print("[!] Asegúrate de haber capturado 'mosi' y 'sck' primero.")
        return

    # Asegurarnos de que están ordenados por tiempo
    mosi_data.sort(key=lambda x: x['t'])
    sck_data.sort(key=lambda x: x['t'])

    bits = []
    
    # Índices para recorrer las listas de forma eficiente
    mosi_idx = 0
    max_mosi_idx = len(mosi_data) - 1

    # Recorremos la señal de RELOJ (SCK)
    # Buscamos cuando pasa de 0 a 1 (Rising Edge)
    for i in range(1, len(sck_data)):
        prev_sck = sck_data[i-1]
        curr_sck = sck_data[i]

        # Detectar Flanco de Subida (0 -> 1)
        if prev_sck['v'] == 0 and curr_sck['v'] == 1:
            sample_time = curr_sck['t']
            
            # Buscar el valor de MOSI en este instante 'sample_time'
            # Avanzamos el índice de MOSI hasta encontrar el segmento correcto
            # El valor válido es el del último evento MOSI que ocurrió antes o en sample_time
            while mosi_idx < max_mosi_idx and mosi_data[mosi_idx+1]['t'] <= sample_time:
                mosi_idx += 1
            
            # Tomamos el valor
            bit_val = mosi_data[mosi_idx]['v']
            bits.append(str(bit_val))

    print(f"[*] Bits extraídos: {len(bits)}")

    # Convertir Bits a Bytes (MSB First para SPI)
    raw_bytes = []
    bit_string = "".join(bits)
    
    for i in range(0, len(bit_string), 8):
        byte_chunk = bit_string[i:i+8]
        if len(byte_chunk) < 8: break
        
        # MSB First: Conversión directa
        val = int(byte_chunk, 2)
        raw_bytes.append(val)

    # Descifrar XOR
    decrypted_chars = []
    for i, byte_val in enumerate(raw_bytes):
        # Usamos el operador módulo % para repetir la clave 'icy'
        key_char = XOR_KEY[i % len(XOR_KEY)]
        decrypted_byte = byte_val ^ ord(key_char)
        
        if 32 <= decrypted_byte <= 126:
            decrypted_chars.append(chr(decrypted_byte))
        else:
            decrypted_chars.append('.')

    print("\n--- MENSAJE DECODIFICADO (SPI) ---")
    print("".join(decrypted_chars))
    print("----------------------------------")

if __name__ == "__main__":
    solve_spi()
```

```bash
python solve-spi.py
[*] Cargando archivos mosi_data.json y sck_data.json...
[*] Bits extraídos: 800

--- MENSAJE DECODIFICADO (SPI) ---
read and decrypt the I2C bus data using the XOR key: bananza. the temperature sensor address is 0x3C
```

### stage 3

solve-ic2.py

```
import asyncio
import websockets
import json

# Configuración
BASE_URL = "wss://signals.holidayhackchallenge.com/wire"
XOR_KEY = "bananza"
TARGET_ADDRESS = 0x3C
CAPTURE_DURATION = 30  # segundos

# ============================================
# PARTE 1: CAPTURA DE DATOS
# ============================================

async def capture_wire(wire_name, duration):
    """Captura datos de un wire específico"""
    url = f"{BASE_URL}/{wire_name}"
    frames = []
    
    print(f"[*] Conectando a {wire_name}...")
    
    try:
        async with websockets.connect(url) as ws:
            print(f"[*] Conectado a {wire_name}. Capturando por {duration} segundos...")
            
            start_time = asyncio.get_event_loop().time()
            
            while asyncio.get_event_loop().time() - start_time < duration:
                try:
                    message = await asyncio.wait_for(ws.recv(), timeout=1.0)
                    data = json.loads(message)
                    
                    if data.get('type') == 'welcome':
                        print(f"[*] {wire_name}: {data.get('message')}")
                        continue
                    
                    if 'line' in data and 't' in data and 'v' in data:
                        frames.append(data)
                        
                        if len(frames) % 100 == 0:
                            print(f"[*] {wire_name}: {len(frames)} frames capturados...")
                
                except asyncio.TimeoutError:
                    continue
            
            print(f"[*] {wire_name}: Captura completa. Total frames: {len(frames)}")
            return frames
            
    except Exception as e:
        print(f"[!] Error capturando {wire_name}: {e}")
        return []

async def capture_i2c_data(duration):
    """Captura SDA y SCL para protocolo I2C"""
    print("\n" + "="*50)
    print("FASE 1: CAPTURA DE DATOS I2C")
    print("="*50)
    print(f"[*] Capturando por {duration} segundos...")
    
    sda_data, scl_data = await asyncio.gather(
        capture_wire('sda', duration),
        capture_wire('scl', duration)
    )
    
    print("\n[*] ¡Captura I2C completa!")
    return sda_data, scl_data

# ============================================
# PARTE 2: DECODIFICACIÓN I2C
# ============================================

def detect_i2c_conditions(sda_data, scl_data):
    """
    Detecta condiciones START y STOP en I2C
    START: SDA cae mientras SCL está alto
    STOP: SDA sube mientras SCL está alto
    """
    conditions = []
    
    sda_idx = 0
    scl_idx = 0
    
    while sda_idx < len(sda_data) - 1:
        sda_curr = sda_data[sda_idx]
        sda_next = sda_data[sda_idx + 1]
        
        # Encuentra el estado de SCL en este tiempo
        while scl_idx < len(scl_data) - 1 and scl_data[scl_idx + 1]['t'] <= sda_curr['t']:
            scl_idx += 1
        
        scl_state = scl_data[scl_idx]['v']
        
        # START: SDA cae (1->0) mientras SCL está alto
        if sda_curr['v'] == 1 and sda_next['v'] == 0 and scl_state == 1:
            conditions.append(('START', sda_next['t']))
        
        # STOP: SDA sube (0->1) mientras SCL está alto
        elif sda_curr['v'] == 0 and sda_next['v'] == 1 and scl_state == 1:
            conditions.append(('STOP', sda_next['t']))
        
        sda_idx += 1
    
    return conditions

def decode_i2c_transactions(sda_data, scl_data, conditions):
    """Decodifica transacciones I2C entre START y STOP"""
    transactions = []
    
    for i in range(len(conditions) - 1):
        if conditions[i][0] != 'START':
            continue
        
        start_time = conditions[i][1]
        
        # Encuentra el STOP correspondiente
        stop_time = None
        for j in range(i + 1, len(conditions)):
            if conditions[j][0] == 'STOP':
                stop_time = conditions[j][1]
                break
        
        if not stop_time:
            continue
        
        # Extrae bits entre START y STOP muestreando en flancos de subida de SCL
        bits = []
        
        sda_idx = 0
        # Encuentra posición inicial de SDA
        while sda_idx < len(sda_data) and sda_data[sda_idx]['t'] < start_time:
            sda_idx += 1
        
        # Procesa flancos de subida de SCL
        for scl_idx in range(1, len(scl_data)):
            scl_prev = scl_data[scl_idx - 1]
            scl_curr = scl_data[scl_idx]
            
            # Salta si está fuera de la ventana de transacción
            if scl_curr['t'] < start_time or scl_curr['t'] > stop_time:
                continue
            
            # Flanco de subida (0 -> 1)
            if scl_prev['v'] == 0 and scl_curr['v'] == 1:
                sample_time = scl_curr['t']
                
                # Encuentra valor de SDA en este tiempo
                while sda_idx < len(sda_data) - 1 and sda_data[sda_idx + 1]['t'] <= sample_time:
                    sda_idx += 1
                
                if sda_idx < len(sda_data):
                    bits.append(sda_data[sda_idx]['v'])
        
        if bits:
            transactions.append(bits)
    
    return transactions

def parse_i2c_bytes(bits):
    """
    Convierte bits I2C en bytes
    Cada 9º bit es ACK/NACK (ignorarlo)
    MSB primero
    """
    bytes_list = []
    byte_bits = []
    bit_count = 0
    
    for bit in bits:
        bit_count += 1
        
        # Cada 9º bit es ACK - saltarlo
        if bit_count % 9 == 0:
            continue
        
        byte_bits.append(str(bit))
        
        # Cuando tenemos 8 bits de datos, convertir a byte
        if len(byte_bits) == 8:
            byte_val = int(''.join(byte_bits), 2)
            bytes_list.append(byte_val)
            byte_bits = []
    
    return bytes_list

def decode_i2c(sda_data, scl_data):
    """Proceso completo de decodificación I2C"""
    print("\n" + "="*50)
    print("FASE 2: DECODIFICACIÓN I2C")
    print("="*50)
    
    # Ordenar por timestamp
    sda_data.sort(key=lambda x: x['t'])
    scl_data.sort(key=lambda x: x['t'])
    
    print(f"[*] Frames SDA: {len(sda_data)}, Frames SCL: {len(scl_data)}")
    
    # Detectar condiciones START/STOP
    print("[*] Detectando condiciones I2C START/STOP...")
    conditions = detect_i2c_conditions(sda_data, scl_data)
    print(f"[*] Encontradas {len(conditions)} condiciones")
    
    # Decodificar transacciones
    print("[*] Decodificando transacciones I2C...")
    transactions = decode_i2c_transactions(sda_data, scl_data, conditions)
    print(f"[*] Encontradas {len(transactions)} transacciones")
    
    # Procesar transacciones
    all_data = []
    
    for trans_idx, bits in enumerate(transactions):
        if len(bits) < 9:  # Necesita al menos byte de dirección + ACK
            continue
        
        bytes_list = parse_i2c_bytes(bits)
        
        if not bytes_list:
            continue
        
        # Primer byte es (dirección de 7 bits << 1) | bit R/W
        first_byte = bytes_list[0]
        address = first_byte >> 1
        rw_bit = first_byte & 0x01
        
        # Filtrar por dirección objetivo
        if address == TARGET_ADDRESS:
            # Bytes de datos (saltar byte de dirección)
            data_bytes = bytes_list[1:]
            all_data.extend(data_bytes)
            print(f"[*] Transacción {trans_idx}: Dirección 0x{address:02X}, R/W={rw_bit}, Bytes de datos: {len(data_bytes)}")
    
    print(f"\n[*] Total de bytes de datos del dispositivo 0x{TARGET_ADDRESS:02X}: {len(all_data)}")
    
    return all_data

# ============================================
# PARTE 3: DESCIFRADO XOR
# ============================================

def xor_decrypt(data_bytes, key):
    """Descifra datos usando XOR con la clave dada"""
    print("\n" + "="*50)
    print("FASE 3: DESCIFRADO XOR")
    print("="*50)
    print(f"[*] Descifrando con clave: '{key}'")
    
    decrypted = []
    
    for i, byte_val in enumerate(data_bytes):
        key_char = key[i % len(key)]
        decrypted_byte = byte_val ^ ord(key_char)
        
        if 32 <= decrypted_byte <= 126:
            decrypted.append(chr(decrypted_byte))
        else:
            # Mostrar hex para no imprimibles
            decrypted.append(f"\\x{decrypted_byte:02x}")
    
    return ''.join(decrypted)

# ============================================
# FUNCIÓN PRINCIPAL
# ============================================

async def main():
    print("\n" + "="*50)
    print("SOLUCIONADOR COMPLETO DE I2C")
    print("="*50)
    print(f"Clave XOR: {XOR_KEY}")
    print(f"Dirección objetivo: 0x{TARGET_ADDRESS:02X}")
    print(f"Duración de captura: {CAPTURE_DURATION} segundos")
    
    # Fase 1: Capturar datos
    sda_data, scl_data = await capture_i2c_data(CAPTURE_DURATION)
    
    if not sda_data or not scl_data:
        print("[!] Error: No se capturaron datos")
        return
    
    # Fase 2: Decodificar I2C
    data_bytes = decode_i2c(sda_data, scl_data)
    
    if not data_bytes:
        print("[!] Error: No se encontraron datos del dispositivo objetivo")
        return
    
    # Fase 3: Descifrar con XOR
    result = xor_decrypt(data_bytes, XOR_KEY)
    
    # Mostrar resultado final
    print("\n" + "="*50)
    print("RESULTADO FINAL")
    print("="*50)
    print(result)
    print("="*50)
    print("\n[✓] ¡Proceso completado!")

if __name__ == "__main__":
    try:
        asyncio.run(main())
    except KeyboardInterrupt:
        print("\n[!] Captura interrumpida por el usuario")
    except Exception as e:
        print(f"\n[!] Error: {e}")
        import traceback
        traceback.print_exc()
```