<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch App</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root {
    --primary-gradient: linear-gradient(135deg, #6cb495 0%, #4b85a2 100%);
    --glass-bg: rgba(255, 255, 255, 0.1);
    --glass-border: rgba(255, 255, 255, 0.2);
    --text-primary: #ffffff;
    --text-secondary: rgba(255, 255, 255, 0.8);
    --shadow-light: 0 8px 32px rgba(0, 0, 0, 0.1);
    --shadow-heavy: 0 20px 60px rgba(0, 0, 0, 0.2);
    --border-radius: 20px;
    --animation-speed: 0.3s;
}

body {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
    background: var(--primary-gradient);
    background-attachment: fixed;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    overflow-x: hidden;
}

body::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: 
        radial-gradient(circle at 20% 50%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
        radial-gradient(circle at 80% 20%, rgba(255, 119, 198, 0.3) 0%, transparent 50%),
        radial-gradient(circle at 40% 80%, rgba(120, 219, 255, 0.3) 0%, transparent 50%);
    z-index: -1;
    animation: backgroundShift 20s ease-in-out infinite;
}

@keyframes backgroundShift {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.8; }
}

.stopwatch-container {
    background: var(--glass-bg);
    backdrop-filter: blur(20px);
    border: 1px solid var(--glass-border);
    border-radius: var(--border-radius);
    padding: 40px;
    box-shadow: var(--shadow-heavy);
    text-align: center;
    max-width: 500px;
    width: 100%;
    animation: slideInUp 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    position: relative;
    overflow: hidden;
}

.stopwatch-container::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
    animation: shimmer 3s infinite;
}

@keyframes slideInUp {
    from {
        opacity: 0;
        transform: translateY(60px) scale(0.95);
    }
    to {
        opacity: 1;
        transform: translateY(0) scale(1);
    }
}

@keyframes shimmer {
    0% { left: -100%; }
    100% { left: 100%; }
}

.display {
    font-size: clamp(2.5rem, 8vw, 4.5rem);
    font-weight: 700;
    color: var(--text-primary);
    margin-bottom: 30px;
    font-family: 'Inter', monospace;
    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(10px);
    padding: 25px;
    border-radius: 16px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    box-shadow: inset 0 2px 4px rgba(255, 255, 255, 0.1);
    letter-spacing: 0.05em;
    transition: all var(--animation-speed) ease;
    position: relative;
    overflow: hidden;
}

.display.running {
    animation: pulse 2s ease-in-out infinite;
    box-shadow: 
        inset 0 2px 4px rgba(255, 255, 255, 0.1),
        0 0 30px rgba(255, 255, 255, 0.2);
}

@keyframes pulse {
    0%, 100% { 
        box-shadow: 
            inset 0 2px 4px rgba(255, 255, 255, 0.1),
            0 0 30px rgba(255, 255, 255, 0.2);
    }
    50% { 
        box-shadow: 
            inset 0 2px 4px rgba(255, 255, 255, 0.2),
            0 0 40px rgba(255, 255, 255, 0.3);
    }
}

.controls {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 12px;
    margin-bottom: 30px;
    padding: 0 10px;
}

button {
    padding: 16px 24px;
    font-size: 1rem;
    font-weight: 600;
    border: none;
    border-radius: 50px;
    cursor: pointer;
    transition: all var(--animation-speed) cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
    color: white;
    font-family: 'Inter', sans-serif;
    min-height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
}

button::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
    transition: left 0.5s;
}

button:hover::before {
    left: 100%;
}

.start-btn {
    background: linear-gradient(135deg, #00f260, #0575e6);
    box-shadow: 0 4px 15px rgba(5, 117, 230, 0.3);
}

.start-btn:hover {
    transform: translateY(-3px) scale(1.02);
    box-shadow: 0 8px 25px rgba(5, 117, 230, 0.4);
}

.start-btn:active {
    transform: translateY(-1px) scale(0.98);
}

.pause-btn {
    background: linear-gradient(135deg, #f093fb, #f5576c);
    box-shadow: 0 4px 15px rgba(245, 87, 108, 0.3);
}

.pause-btn:hover {
    transform: translateY(-3px) scale(1.02);
    box-shadow: 0 8px 25px rgba(245, 87, 108, 0.4);
}

.reset-btn {
    background: linear-gradient(135deg, #4facfe, #00f2fe);
    box-shadow: 0 4px 15px rgba(79, 172, 254, 0.3);
}

.reset-btn:hover {
    transform: translateY(-3px) scale(1.02);
    box-shadow: 0 8px 25px rgba(79, 172, 254, 0.4);
}

.lap-btn {
    background: linear-gradient(135deg, #a8edea, #fed6e3);
    color: #333;
    box-shadow: 0 4px 15px rgba(168, 237, 234, 0.3);
}

.lap-btn:hover {
    transform: translateY(-3px) scale(1.02);
    box-shadow: 0 8px 25px rgba(168, 237, 234, 0.4);
}

button:disabled {
    opacity: 0.4;
    cursor: not-allowed;
    transform: none !important;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1) !important;
}

button:disabled::before {
    display: none;
}

.lap-times {
    max-height: 350px;
    overflow-y: auto;
    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(10px);
    border-radius: 16px;
    padding: 20px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    animation: fadeInUp 0.6s ease 0.3s both;
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.lap-times h3 {
    color: var(--text-primary);
    margin-bottom: 20px;
    font-size: 1.2rem;
    font-weight: 600;
}

.lap-times::-webkit-scrollbar {
    width: 6px;
}

.lap-times::-webkit-scrollbar-track {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 3px;
}

.lap-times::-webkit-scrollbar-thumb {
    background: rgba(255, 255, 255, 0.3);
    border-radius: 3px;
}

.lap-times::-webkit-scrollbar-thumb:hover {
    background: rgba(255, 255, 255, 0.5);
}

.lap-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px 20px;
    margin: 8px 0;
    background: rgba(255, 255, 255, 0.08);
    backdrop-filter: blur(10px);
    border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    transition: all var(--animation-speed) ease;
    animation: slideInLeft 0.4s ease;
}

@keyframes slideInLeft {
    from {
        opacity: 0;
        transform: translateX(-20px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

.lap-item:hover {
    background: rgba(255, 255, 255, 0.12);
    transform: translateX(5px);
}

.lap-number {
    font-weight: 600;
    color: var(--text-primary);
    font-size: 0.9rem;
}

.lap-time {
    font-family: 'Inter', monospace;
    font-weight: 600;
    color: var(--text-secondary);
    font-size: 1rem;
}

.no-laps {
    color: var(--text-secondary);
    font-style: italic;
    padding: 20px;
    text-align: center;
}

/* Responsive Design */
@media (max-width: 768px) {
    .stopwatch-container {
        padding: 30px 20px;
        margin: 10px;
    }
    
    .display {
        padding: 20px 15px;
        margin-bottom: 25px;
    }
    
    .controls {
        grid-template-columns: 1fr 1fr;
        gap: 10px;
    }
    
    button {
        padding: 14px 18px;
        font-size: 0.9rem;
        min-height: 50px;
    }
}

@media (max-width: 480px) {
    body {
        padding: 10px;
    }
    
    .stopwatch-container {
        padding: 25px 15px;
    }
    
    .controls {
        grid-template-columns: 1fr;
        gap: 8px;
    }
    
    .lap-times {
        max-height: 250px;
        padding: 15px;
    }
    
    .lap-item {
        padding: 12px 15px;
        flex-direction: column;
        gap: 5px;
        text-align: center;
    }
}

@media (max-width: 320px) {
    .display {
        padding: 15px 10px;
    }
    
    button {
        padding: 12px 15px;
        font-size: 0.85rem;
        min-height: 45px;
    }
}

/* Accessibility */
@media (prefers-reduced-motion: reduce) {
    * {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
    }
    
    .display.running {
        animation: none;
    }
    
    body::before {
        animation: none;
    }
}

/* Focus states for accessibility */
button:focus-visible {
    outline: 2px solid rgba(255, 255, 255, 0.8);
    outline-offset: 2px;
}

/* High contrast mode support */
@media (prefers-contrast: high) {
    :root {
        --glass-bg: rgba(0, 0, 0, 0.8);
        --glass-border: rgba(255, 255, 255, 0.8);
        --text-primary: #ffffff;
        --text-secondary: #ffffff;
    }
}
    </style>
</head>
<body>
    <div class="stopwatch-container">
        <div class="display" id="display">00:00:00</div>
        
        <div class="controls">
            <button class="start-btn" id="startBtn">Start</button>
            <button class="pause-btn" id="pauseBtn" disabled>Pause</button>
            <button class="reset-btn" id="resetBtn">Reset</button>
            <button class="lap-btn" id="lapBtn" disabled>Lap</button>
        </div>
        
        <div class="lap-times">
            <h3>Lap Times</h3>
            <div id="lapList">
                <div class="no-laps">No lap times recorded yet</div>
            </div>
        </div>
    </div>
    
    <script>
        class Stopwatch {
  constructor() {
    // Initialize properties
    this.startTime = 0;
    this.elapsedTime = 0;
    this.timerInterval = null;
    this.isRunning = false;
    this.lapTimes = [];
    this.lapCounter = 0;

    // Wait for DOM to be ready before initializing
    if (document.readyState === "loading") {
      document.addEventListener("DOMContentLoaded", () => this.init());
    } else {
      this.init();
    }
  }

  init() {
    try {
      this.initializeElements();
      this.attachEventListeners();
      this.updateDisplay();
      console.log("Stopwatch initialized successfully");
    } catch (error) {
      console.error("Error initializing stopwatch:", error);
    }
  }

  initializeElements() {
    // Get DOM elements with error checking
    this.display = this.getElement("display");
    this.startBtn = this.getElement("startBtn");
    this.pauseBtn = this.getElement("pauseBtn");
    this.resetBtn = this.getElement("resetBtn");
    this.lapBtn = this.getElement("lapBtn");
    this.lapList = this.getElement("lapList");

    // Verify all elements exist
    if (
      !this.display ||
      !this.startBtn ||
      !this.pauseBtn ||
      !this.resetBtn ||
      !this.lapBtn ||
      !this.lapList
    ) {
      throw new Error("One or more required DOM elements not found");
    }
  }

  getElement(id) {
    const element = document.getElementById(id);
    if (!element) {
      console.error(`Element with id '${id}' not found`);
    }
    return element;
  }

  attachEventListeners() {
    // Use arrow functions to maintain 'this' context
    this.startBtn.addEventListener("click", (e) => {
      e.preventDefault();
      this.start();
    });

    this.pauseBtn.addEventListener("click", (e) => {
      e.preventDefault();
      this.pause();
    });

    this.resetBtn.addEventListener("click", (e) => {
      e.preventDefault();
      this.reset();
    });

    this.lapBtn.addEventListener("click", (e) => {
      e.preventDefault();
      this.recordLap();
    });

    // Add keyboard support
    document.addEventListener("keydown", (e) => this.handleKeyPress(e));
  }

  handleKeyPress(event) {
    // Add keyboard shortcuts
    switch (event.code) {
      case "Space":
        event.preventDefault();
        if (this.isRunning) {
          this.pause();
        } else {
          this.start();
        }
        break;
      case "KeyR":
        if (event.ctrlKey || event.metaKey) {
          event.preventDefault();
          this.reset();
        }
        break;
      case "KeyL":
        if (this.isRunning) {
          event.preventDefault();
          this.recordLap();
        }
        break;
    }
  }

  start() {
    try {
      if (!this.isRunning) {
        this.startTime = performance.now() - this.elapsedTime;
        this.timerInterval = setInterval(() => this.updateDisplay(), 10);
        this.isRunning = true;

        this.updateButtonStates();
        console.log("Stopwatch started");
      }
    } catch (error) {
      console.error("Error starting stopwatch:", error);
    }
  }

  pause() {
    try {
      if (this.isRunning) {
        clearInterval(this.timerInterval);
        this.timerInterval = null;
        this.isRunning = false;

        this.updateButtonStates();
        console.log("Stopwatch paused");
      }
    } catch (error) {
      console.error("Error pausing stopwatch:", error);
    }
  }

  reset() {
    try {
      // Clear any existing interval
      if (this.timerInterval) {
        clearInterval(this.timerInterval);
        this.timerInterval = null;
      }

      // Reset all properties
      this.isRunning = false;
      this.elapsedTime = 0;
      this.startTime = 0;
      this.lapTimes = [];
      this.lapCounter = 0;

      // Update display and UI
      this.updateDisplay();
      this.updateLapDisplay();
      this.updateButtonStates();

      console.log("Stopwatch reset");
    } catch (error) {
      console.error("Error resetting stopwatch:", error);
    }
  }

  recordLap() {
    try {
      if (this.isRunning) {
        this.lapCounter++;
        const lapTime = this.elapsedTime;

        // Add lap with additional metadata
        this.lapTimes.push({
          number: this.lapCounter,
          time: lapTime,
          timestamp: new Date().toISOString(),
        });

        this.updateLapDisplay();
        console.log(
          `Lap ${this.lapCounter} recorded: ${this.formatTime(lapTime)}`
        );
      }
    } catch (error) {
      console.error("Error recording lap:", error);
    }
  }

  updateDisplay() {
    try {
      if (this.isRunning) {
        this.elapsedTime = performance.now() - this.startTime;
      }

      const formattedTime = this.formatTime(this.elapsedTime);
      if (this.display) {
        this.display.textContent = formattedTime;

        // Add/remove running animation class
        if (this.isRunning) {
          this.display.classList.add("running");
        } else {
          this.display.classList.remove("running");
        }
      }
    } catch (error) {
      console.error("Error updating display:", error);
    }
  }

  updateLapDisplay() {
    try {
      if (!this.lapList) return;

      if (this.lapTimes.length === 0) {
        this.lapList.innerHTML =
          '<div class="no-laps">No lap times recorded yet</div>';
        return;
      }

      // Create lap items HTML with error handling
      const lapItemsHTML = this.lapTimes
        .slice()
        .reverse()
        .map((lap) => {
          const formattedTime = this.formatTime(lap.time);
          return `
                        <div class="lap-item" data-lap="${lap.number}">
                            <span class="lap-number">Lap ${lap.number}</span>
                            <span class="lap-time">${formattedTime}</span>
                        </div>
                    `;
        })
        .join("");

      this.lapList.innerHTML = lapItemsHTML;
    } catch (error) {
      console.error("Error updating lap display:", error);
      if (this.lapList) {
        this.lapList.innerHTML =
          '<div class="no-laps">Error displaying lap times</div>';
      }
    }
  }

  updateButtonStates() {
    try {
      if (this.startBtn) this.startBtn.disabled = this.isRunning;
      if (this.pauseBtn) this.pauseBtn.disabled = !this.isRunning;
      if (this.lapBtn) this.lapBtn.disabled = !this.isRunning;
      if (this.resetBtn) this.resetBtn.disabled = false; // Reset is always available
    } catch (error) {
      console.error("Error updating button states:", error);
    }
  }

  formatTime(milliseconds) {
    try {
      // Ensure milliseconds is a valid number
      const ms = Math.max(0, Math.floor(milliseconds));

      const totalSeconds = Math.floor(ms / 1000);
      const minutes = Math.floor(totalSeconds / 60);
      const seconds = totalSeconds % 60;
      const centiseconds = Math.floor((ms % 1000) / 10);

      // Use padStart for consistent formatting
      return `${minutes.toString().padStart(2, "0")}:${seconds
        .toString()
        .padStart(2, "0")}:${centiseconds.toString().padStart(2, "0")}`;
    } catch (error) {
      console.error("Error formatting time:", error);
      return "00:00:00";
    }
  }

  // Public method to get current state (useful for debugging)
  getState() {
    return {
      isRunning: this.isRunning,
      elapsedTime: this.elapsedTime,
      formattedTime: this.formatTime(this.elapsedTime),
      lapCount: this.lapTimes.length,
      lapTimes: this.lapTimes.map((lap) => ({
        number: lap.number,
        formattedTime: this.formatTime(lap.time),
      })),
    };
  }

  // Public method to destroy the stopwatch (cleanup)
  destroy() {
    try {
      if (this.timerInterval) {
        clearInterval(this.timerInterval);
        this.timerInterval = null;
      }

      // Remove event listeners
      document.removeEventListener("keydown", this.handleKeyPress);

      console.log("Stopwatch destroyed");
    } catch (error) {
      console.error("Error destroying stopwatch:", error);
    }
  }
}

// Initialize the stopwatch when the page loads
let stopwatchInstance = null;

// Function to initialize stopwatch
function initializeStopwatch() {
  try {
    if (stopwatchInstance) {
      stopwatchInstance.destroy();
    }
    stopwatchInstance = new Stopwatch();
  } catch (error) {
    console.error("Failed to initialize stopwatch:", error);
  }
}

// Multiple initialization methods to ensure compatibility
if (document.readyState === "loading") {
  document.addEventListener("DOMContentLoaded", initializeStopwatch);
} else {
  initializeStopwatch();
}

// Fallback initialization
window.addEventListener("load", () => {
  if (!stopwatchInstance) {
    initializeStopwatch();
  }
});

// Export for module systems (if needed)
if (typeof module !== "undefined" && module.exports) {
  module.exports = Stopwatch;
}

// Global access for debugging
window.Stopwatch = Stopwatch;
window.stopwatchInstance = stopwatchInstance;
    </script>
</body>
</html>
