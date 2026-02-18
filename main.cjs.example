const { app, BrowserWindow } = require("electron");
const { spawn } = require("child_process");
const path = require("path");
const os = require("os");

let mainWindow;
let pythonProcess;

function startBackend() {
  // Manjaro often puts uv in ~/.local/bin/
  // This looks for the uv binary specifically in your user folder
  const uvPath = path.join(os.homedir(), ".local/bin/uv");

  console.log(`Attempting to start engine at: ${uvPath}`);

  pythonProcess = spawn(uvPath, ["run", "fastapi", "dev", "main.py"], {
    cwd: path.join(__dirname, "../backend"),
    shell: true,
    env: {
      ...process.env,
      PATH: `${process.env.PATH}:${path.join(os.homedir(), ".local/bin")}`,
    },
  });

  pythonProcess.stdout.on("data", (data) => console.log(`[Python]: ${data}`));
  pythonProcess.stderr.on("data", (data) =>
    console.error(`[Python Error]: ${data}`),
  );
}

function createWindow() {
  mainWindow = new BrowserWindow({
    width: 1100,
    height: 700,
    webPreferences: {
      nodeIntegration: false,
      contextIsolation: true,
    },
  });

  // Point to Vite
  mainWindow.loadURL("http://localhost:5173");

  mainWindow.on("closed", () => {
    mainWindow = null;
  });
}

app.whenReady().then(() => {
  startBackend();
  createWindow();
});

app.on("will-quit", () => {
  if (pythonProcess) {
    console.log("Terminating Python Engine...");
    pythonProcess.kill("SIGINT");
  }
});

app.on("window-all-closed", () => {
  if (process.platform !== "darwin") app.quit();
});
