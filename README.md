# Pip Speed Tester

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-blue.svg" alt="Python Version">
  <img src="https://img.shields.io/badge/React-18.2-61dafb.svg" alt="React Version">
  <img src="https://img.shields.io/badge/Flask-2.3-000000.svg" alt="Flask Version">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License">
</p>

<p align="center">
  <strong>A Web Tool for Testing and Selecting Optimal PyPI Sources</strong>
</p>

<p align="center">
  <img src="https://wwwwww344.github.io/" alt="Interface Preview" width="800">
</p>

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Technical Architecture](#technical-architecture)
- [Supported pip Sources](#supported-pip-sources)
- [Quick Start](#quick-start)
- [Installation Guide](#installation-guide)
- [Configuration](#configuration)
- [API Documentation](#api-documentation)
- [How It Works](#how-it-works)
- [FAQ](#faq)
- [Performance Optimization](#performance-optimization)
- [Project Structure](#project-structure)
- [Contributing](#contributing)
- [Changelog](#changelog)
- [Disclaimer](#disclaimer)
- [Acknowledgements](#acknowledgements)
- [Contact](#contact)

## Introduction

Pip Speed Tester is a pip source testing tool designed specifically for developers in China. It helps users quickly find the optimal PyPI mirror source to accelerate Python package download and installation processes.

In mainland China, due to special network environments, direct access to the official PyPI source often results in slow speeds. Various universities, cloud service providers, and open-source organizations have set up pip mirror sources, but network latency varies significantly due to geographic location and network线路. This tool performs actual network speed tests to help users choose the optimal pip source and improve Python development efficiency.

The design of this tool was inspired by the [cnpip](https://github.com/sunny5261/cnpm) project, but uses a modern Web technology stack for reconstruction, providing a more friendly user interface and more stable speed testing services.

### Why pip Source Speed Testing is Needed

When developing with Python, we often need to install various third-party packages. Using the default PyPI official source may face the following problems in domestic network environments:

1. **Slow Download Speed**: High cross-border network latency leads to slow package downloads
2. **Unstable Connections**: Frequent connection timeouts or download interruptions
3. **Poor User Experience**: Long waiting times affect development efficiency

By testing and selecting the optimal domestic mirror source, download speed can be improved several times or even dozens of times, significantly improving the Python package management experience.

## Features

### 1. Real Network Speed Testing

This tool uses real HTTP HEAD requests to measure response latency of each pip source, not simulated or random data. Each speed test will:

- Send HTTP HEAD requests to target sources
- Measure the time interval from request sending to response receiving
- Perform multiple tests and take the average to eliminate network fluctuation effects
- Automatically handle redirects and timeout situations

### 2. Multi-Source Concurrent Testing

The tool supports simultaneous testing of multiple pip sources, implementing concurrent speed testing through ThreadPoolExecutor, significantly reducing speed testing time:

- Supports simultaneous testing of 20+ pip sources
- Configurable concurrent thread count (default: 5)
- Real-time display of testing progress
- Automatic retry on test failure

### 3. Intelligent Optimal Source Recommendation

After speed testing is complete, the tool automatically identifies the pip source with the lowest latency and displays the recommendation results in a prominent card format. The recommendation algorithm comprehensively considers:

- Average response latency
- Test success rate
- Historical test data

### 4. One-Click Copy Installation Commands

For the recommended optimal source, the tool provides two pip configuration methods:

**Temporary Installation Command**:
```bash
pip install <package> -i <source-url>
```

**Global Configuration Command**:
```bash
pip config set global.index-url <source-url>
```

Users can simply click the copy button to paste the command into the terminal for execution.

### 5. Automatic Region Detection

The tool automatically detects the user's geographic location and displays the current network node information. Users can also manually select different testing regions to obtain more accurate speed test results.

Automatically detected regions include:

- Major Chinese cities (Beijing, Shanghai, Guangzhou, Shenzhen, etc.)
- Hong Kong, China; Taiwan, China
- United States, Japan, Singapore, Europe, and other overseas nodes

### 6. History Record Saving

The tool automatically saves recent speed test history records, including:

- Test time
- Test region
- Optimal source and latency

Convenient for users to review historical test results and compare network conditions at different time periods.

### 7. Responsive Web Interface

The tool provides a modern responsive Web interface, supporting:

- Desktop and mobile adaptive design
- Dark mode adaptation
- Smooth animation effects
- Intuitive visual latency bars

### 8. Complete API Interface

In addition to the Web interface, the tool also provides a complete RESTful API interface, supporting:

- Automated speed testing script integration
- Source quality monitoring in CI/CD processes
- Third-party application integration

## Technical Architecture

### Frontend Technology Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| React | 18.2.0 | UI Component Framework |
| Vite | 5.4.0 | Build Tool |
| Axios | 1.6.2 | HTTP Client |
| Chart.js | latest | Data Visualization |
| React Icons | latest | Icon Library |
| React Dropzone | latest | File Drag and Drop |

### Backend Technology Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| Flask | 2.3.0 | Web Framework |
| Flask-CORS | 3.0.10 | Cross-Origin Resource Sharing |
| requests | latest | HTTP Client |
| concurrent.futures | standard library | Concurrent Execution |

### System Architecture

### Technical Features

1. **Frontend-Backend Separation Architecture**: Frontend built with React, backend provides API services with Flask, clear responsibilities
2. **Concurrent Speed Testing Optimization**: Using thread pool for concurrent testing, fully utilizing network I/O parallelism
3. **Result Caching Mechanism**: Speed test results are cached for a period of time to avoid frequent testing causing server pressure
4. **Cross-Origin Support**: CORS configured for easy frontend-backend separation development and deployment
5. **Comprehensive Exception Handling**: Global exception capture to ensure stable service operation

## Supported pip Sources

This tool integrates the following pip mirror sources, displayed sorted by latency:

### Domestic Official Mirror Sources

| Name | URL | Maintainer |
|------|-----|------------|
| Aliyun | https://mirrors.aliyun.com/pypi/simple | Alibaba |
| Tsinghua TUNA | https://pypi.tuna.tsinghua.edu.cn/simple | Tsinghua University TUNA Association |
| Tencent Cloud | https://mirrors.cloud.tencent.com/pypi/simple | Tencent Cloud |
| Huawei Cloud | https://repo.huaweicloud.com/repository/pypi/simple | Huawei Cloud |
| Douban | https://pypi.doubanio.com/simple | Douban |
| NetEase | https://mirrors.163.com/pypi/simple | NetEase |
| Baidu | https://mirror.baidu.com/pypi/simple | Baidu |

### Domestic University Mirror Sources

| Name | URL | Maintainer |
|------|-----|------------|
| USTC | https://pypi.mirrors.ustc.edu.cn/simple | University of Science and Technology of China |
| SJTU | https://mirror.sjtu.edu.cn/pypi/simple | Shanghai Jiao Tong University |
| HUST | https://pypi.hust.edu.cn/simple | Huazhong University of Science and Technology |
| BIT | https://pypi.bit.edu.cn/simple | Beijing Institute of Technology |
| DUT | https://pypi.dut.edu.cn/simple | Dalian University of Technology |
| Neusoft | https://mirrors.neusoft.edu.cn/simple | Dalian Neusoft University of Information |
| LZU | https://pypi.lzu.edu.cn/simple | Lanzhou University |
| Xidian | https://pypi.xidian.edu.cn/simple | Xidian University |
| NJU | https://pypi.nju.edu.cn/simple | Nanjing University |
| CAS | https://pypi.mirrors.casct.com/simple | Chinese Academy of Sciences |
| ZJU | https://pypi.zju.edu.cn/simple | Zhejiang University |

### Official and Overseas Mirror Sources

| Name | URL | Maintainer |
|------|-----|------------|
| Official | https://pypi.org/simple | PyPI Official |
| PyPI Germany | https://pypi.tu-dresden.de/simple | TU Dresden |

### Community Mirror Sources

| Name | URL | Maintainer |
|------|-----|------------|
| BH6BHG's Wireless Power | https://bc9ce2eff4cc.ngrok-free.app/simple | BH6BHG |

**Note**: Community mirror sources may be unstable. Please confirm availability before use.

## Quick Start

### Environment Requirements

Before starting, please ensure your system meets the following requirements:

- **Operating System**: Windows 7+/macOS 10.14+/Linux (Ubuntu 18.04+)
- **Python**: 3.8 or higher
- **Node.js**: 16.0 or higher
- **npm**: 7.0 or higher (or use yarn)
- **Network**: Internet access available

### Step 1: Install Dependencies

#### 1.1 Install Python Dependencies

```bash
# Enter backend directory
cd backend

# Create virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

**requirements.txt content**:

#### 1.2 Install Node.js Dependencies

```bash
# Enter frontend directory
cd ../frontend

# Install dependencies
npm install

# Or use yarn
yarn install
```

### Step 2: Start Services

#### 2.1 Development Mode

```bash
# Terminal 1: Start backend service
cd backend
python app.py

# Terminal 2: Start frontend dev server
cd frontend
npm run dev
```

#### 2.2 Production Mode

```bash
# Build frontend
cd frontend
npm run build

# Start backend service (will serve static files automatically)
cd ../backend
python app.py
```

### Step 3: Access Application

Open browser and visit: `http://localhost:3000`

You should see the following interface:

- Page header shows "Pip Source Speed Test"
- Automatically detects current network node
- Displays "Start cnpip Speed Test" button
- Ready to execute speed test

## Installation Guide

### Windows System Installation

#### Step 1: Install Python

1. Visit [Python Official Website](https://www.python.org/downloads/)
2. Download Python 3.8 or higher installer
3. Run installer, **remember to check "Add Python to PATH"**
4. Verify installation: `python --version`

#### Step 2: Install Node.js

1. Visit [Node.js Official Website](https://nodejs.org/)
2. Download LTS version (recommended 18.x or higher)
3. Run installer
4. Verify installation: `node --version` and `npm --version`

#### Step 3: Clone Project

```bash
# Clone project
git clone https://github.com/yourusername/pip-speed-tester.git
cd pip-speed-tester
```

#### Step 4: Install Backend Dependencies

```bash
cd backend

# Upgrade pip (optional but recommended)
python -m pip install --upgrade pip

# Install dependencies
pip install flask flask-cors requests flask-jwt-extended flask-sqlalchemy pyjwt psycopg2-binary httpx pandas bcrypt

# If you encounter permission issues, use --user parameter
pip install --user flask flask-cors requests flask-jwt-extended flask-sqlalchemy pyjwt psycopg2-binary httpx pandas bcrypt
```

#### Step 5: Install Frontend Dependencies

```bash
cd ../frontend

# Install using npm
npm install

# Or use Taobao mirror for acceleration (recommended in China)
npm install --registry=https://registry.npmmirror.com
```

#### Step 6: Start Services

```bash
# Start backend
cd ../backend
python app.py

# Open a new terminal, start frontend
cd ../frontend
npm run dev
```

### macOS System Installation

```bash
# Install Python and Node.js using Homebrew (if not installed)
brew install python node

# Clone project
git clone https://github.com/yourusername/pip-speed-tester.git
cd pip-speed-tester

# Install backend dependencies
cd backend
python -m pip install -r requirements.txt

# Install frontend dependencies
cd ../frontend
npm install

# Start services
# Terminal 1
cd ../backend && python app.py

# Terminal 2
cd ../frontend && npm run dev
```

### Linux System Installation

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip nodejs npm git

# Clone project
git clone https://github.com/yourusername/pip-speed-tester.git
cd pip-speed-tester

# Install backend dependencies
cd backend
python3 -m pip install -r requirements.txt

# Install frontend dependencies
cd ../frontend
sudo npm install -g npm  # Upgrade npm
npm install

# Start services
# Terminal 1
cd ../backend && python3 app.py

# Terminal 2
cd ../frontend && npm run dev
```

### Docker Deployment (Optional)

If you don't want to install dependencies locally, you can use Docker for deployment:

```dockerfile
# Dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY backend/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY frontend/dist/ frontend/public/ ./backend/

EXPOSE 3000

CMD ["python", "backend/app.py"]
```

```bash
# Build and run
docker build -t pip-speed-tester .
docker run -p 3000:3000 pip-speed-tester
```

## Configuration

### Environment Variable Configuration

You can configure the application through environment variables:

| Environment Variable | Default Value | Description |
|----------------------|---------------|-------------|
| PORT | 3000 | Service port |
| DEBUG | False | Debug mode |
| FLASK_ENV | production | Flask environment |

**Example**:

```bash
# Linux/macOS
export PORT=8080
export DEBUG=True
python app.py

# Windows
set PORT=8080
set DEBUG=True
python app.py
```

### Backend Configuration

You can modify the following configurations in `backend/app.py`:

```python
# pip source configuration
PIP_SOURCES = [
    {"name": "Source Name", "url": "Source URL"},
    # Add or remove sources...
]

# Speed test parameters
def test_pip_source_speed(source, retry_count=3, timeout=3):
    # retry_count: retry times
    # timeout: timeout in seconds
    ...
```

### Frontend Configuration

Frontend configuration is mainly in `frontend/vite.config.mjs`:

```javascript
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:3000',
        changeOrigin: true
      }
    }
  }
})
```

## API Documentation

### 1. Execute pip Source Speed Test

**Endpoint**: `POST /api/speed-test`

**Request Headers**:

**Request Body**:
```json
{
  "region": "China Beijing"
}
```

**Response Example**:
```json
{
  "success": true,
  "sources": [
    {
      "name": "Tsinghua TUNA",
      "url": "https://pypi.tuna.tsinghua.edu.cn/simple",
      "latency": 15,
      "status": "success"
    },
    {
      "name": "Aliyun",
      "url": "https://mirrors.aliyun.com/pypi/simple",
      "latency": 22,
      "status": "success"
    }
  ],
  "fastest": {
    "name": "Tsinghua TUNA",
    "url": "https://pypi.tuna.tsinghua.edu.cn/simple",
    "latency": 15,
    "status": "success"
  },
  "timestamp": "2024-01-15T10:30:00.000Z"
}
```

### 2. Generate pip Installation Command

**Endpoint**: `POST /api/set-source`

**Request Body**:
```json
{
  "source": "Tsinghua TUNA"
}
```

**Response Example**:
```json
{
  "success": true,
  "source": {
    "name": "Tsinghua TUNA",
    "url": "https://pypi.tuna.tsinghua.edu.cn/simple"
  },
  "commands": {
    "temp": "pip install <package> -i https://pypi.tuna.tsinghua.edu.cn/simple",
    "global": "pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple"
  }
}
```

### 3. Health Check

**Endpoint**: `GET /api/health`

**Response Example**:
```json
{
  "status": "ok",
  "service": "pip-speed-tester",
  "timestamp": "2024-01-15T10:30:00.000Z"
}
```

### 4. Error Response Format

**Error Response**:
```json
{
  "success": false,
  "error": "Error description",
  "message": "User-friendly error message"
}
```

**HTTP Status Codes**:
- 200: Success
- 400: Bad Request
- 404: Not Found
- 500: Internal Server Error

## How It Works

### Speed Test Flow

### Speed Test Algorithm

```python
def test_pip_source_speed(source, retry_count=3, timeout=3):
    """
    Speed test algorithm description:
    1. Send warm-up request (not timed)
    2. Send 3 test requests (configurable)
    3. Filter responses with HTTP status code >= 400
    4. Calculate average latency of successful requests
    5. Return -1 (timeout) if all requests fail
    """
    
    # Warm-up request
    try:
        requests.head(url, timeout=timeout)
    except Exception:
        pass
    
    # Formal speed test
    for _ in range(retry_count):
        try:
            start_time = time.time()
            response = requests.head(url, timeout=timeout)
            elapsed = (time.time() - start_time) * 1000  # Convert to milliseconds
            
            if response.status_code < 400:
                total_latency += elapsed
                success_count += 1
        except requests.Timeout:
            pass
    
    # Calculate average latency
    if success_count > 0:
        avg_latency = total_latency / success_count
        return {"latency": avg_latency, "status": "success"}
    else:
        return {"latency": -1, "status": "timeout"}
```

### Why Use HTTP HEAD

HTTP HEAD request is a lightweight request method that:

1. **Only获取响应头**: Does not download response body, significantly reducing network transmission
2. **Fast**: Faster than GET requests
3. **Safe**: Will not trigger server-side package list generation logic
4. **Effective**: Can accurately measure network latency

### Concurrent Speed Test Optimization

The tool uses `ThreadPoolExecutor` for concurrent speed testing:

```python
from concurrent.futures import ThreadPoolExecutor

# Create thread pool, max concurrency 5
with ThreadPoolExecutor(max_workers=5) as executor:
    # Submit all speed test tasks
    future_to_source = {
        executor.submit(test_pip_source_speed, source): source 
        for source in PIP_SOURCES
    }
    
    # Collect results
    for future in as_completed(future_to_source):
        result = future.result()
        results.append(result)
```

**Advantages of concurrent speed testing**:

- Sequential testing of 20 sources takes 60+ seconds (3 seconds timeout per source)
- Concurrent testing takes only 3-5 seconds (5 concurrent)
- Significantly improves user experience

## FAQ

### Q1: Speed test results don't match actual download speed?

**Reason**: Speed test uses HTTP HEAD requests, only measuring network latency. Actual download speed is also affected by:

- Package file size
- Server bandwidth
- Network congestion level
- Concurrent download count

**Suggestion**: Speed test results are for reference only when choosing sources. Actual installation speed should be used as the standard.

### Q2: Some sources show "timeout"?

**Possible reasons**:

1. **Source server down**: Server temporarily unavailable
2. **Network blocked**: Source blocked by firewall
3. **URL changed**: Source address has changed
4. **ngrok free version limitations**: Free ngrok sessions have time limits

**Suggestion**: Try other sources, or retry later.

### Q3: How to add custom pip source?

Edit the `PIP_SOURCES` list in `backend/app.py`:

```python
PIP_SOURCES = [
    # Existing sources...
    
    # Add custom source
    {
        "name": "Custom Source Name",
        "url": "https://your-mirror.example.com/simple"
    },
]
```

### Q4: Speed test button click has no effect?

**Troubleshooting steps**:

1. Check if backend service is running
2. Check browser console for errors
3. Check network connection
4. Refresh page and retry

### Q5: How to clear frontend cache?

Frontend caches speed test history to localStorage. Clearing method:

1. Open browser developer tools (F12)
2. Switch to Application panel
3. Find Local Storage
4. Delete `pip_speed_history` entry

Or use JavaScript:

```javascript
localStorage.removeItem('pip_speed_history');
```

### Q6: How to use in CI/CD?

```bash
# Install dependencies
pip install requests

# Write speed test script
python -c "
import requests
import json

response = requests.post('http://localhost:3000/api/speed-test')
data = response.json()

if data['success']:
    fastest = data['fastest']
    print(f'Fastest source: {fastest[\"name\"]} - {fastest[\"latency\"]}ms')
    
    # Set pip source
    import subprocess
    subprocess.run([
        'pip', 'config', 'set', 'global.index-url', fastest['url']
    ])
"
```

### Q7: Backend fails to start?

**Common errors**:

1. **Port in use**:
   ```bash
   # Windows
   netstat -ano | findstr :3000
   
   # Linux/macOS
   lsof -i :3000
   ```

2. **Module not found**:
   ```bash
   pip install flask flask-cors requests
   ```

3. **Permission issues**:
   ```bash
   pip install --user <package-name>
   ```

### Q8: How to view detailed logs?

Backend logs are output to console by default. Log level can be configured in `app.py`:

```python
logging.basicConfig(
    level=logging.DEBUG,  # Change to DEBUG for more detailed logs
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
```

## Performance Optimization

### Backend Optimization Suggestions

1. **Increase concurrency**:
   ```python
   # Adjust based on server performance
   with ThreadPoolExecutor(max_workers=10) as executor:
   ```

2. **Reduce timeout**:
   ```python
   # If network environment is good, reduce timeout
   timeout = 2  # Originally 3 seconds
   ```

3. **Increase cache time**:
   ```python
   # Change cache time from 1 hour to 24 hours
   cache_key = datetime.now().strftime("%Y%m%d")  # Cache by day
   ```

### Frontend Optimization Suggestions

1. **Production build**:
   ```bash
   npm run build
   ```

2. **Use CDN**:
   Configure CDN to load static resources in `index.html`

3. **Enable Gzip compression**:
   Enable compression in Web server configuration

### Server Optimization Suggestions

1. **Use Nginx reverse proxy**:
   ```nginx
   server {
       listen 80;
       server_name your-domain.com;
       
       location / {
           proxy_pass http://localhost:3000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
       }
   }
   ```

2. **Configure SSL certificate**:
   Use Let's Encrypt free certificate

3. **Use PM2 for process management**:
   ```bash
   npm install -g pm2
   pm2 start app.py --name pip-speed-tester
   ```

## Project Structure

### Directory Description

| Directory/File | Description |
|----------------|-------------|
| `backend/` | Backend service code |
| `frontend/` | Frontend React application |
| `backend/app.py` | Flask main application, contains all API and speed test logic |
| `backend/requirements.txt` | Python dependency list |
| `frontend/src/` | Frontend source code |
| `frontend/src/components/` | React components |
| `frontend/package.json` | npm project configuration |
| `frontend/vite.config.mjs` | Vite build configuration |

## Contributing

Contributions are welcome! Please follow these steps:

### 1. Fork the Project

Click the Fork button in the upper right corner of the project page.

### 2. Clone Your Fork

```bash
git clone https://github.com/YOUR_USERNAME/pip-speed-tester.git
cd pip-speed-tester
```

### 3. Create a Branch

```bash
git checkout -b feature/your-feature-name
```

### 4. Modify Code

Ensure code follows these standards:

- Python code follows PEP 8
- JavaScript code follows ESLint rules
- Add appropriate comments
- Update related documentation

### 5. Commit Changes

```bash
git add .
git commit -m "Add: your feature description"
```

### 6. Push and Create PR

```bash
git push origin feature/your-feature-name
```

Then create a Pull Request on GitHub.

### Contribution Suggestions

The following types of contributions are welcome:

- 🐛 Report bugs
- 💡 Propose new feature suggestions
- 📝 Improve documentation
- 🔧 Submit code fixes
- 🎨 Improve user interface
- 🌐 Add new pip mirror sources
- 🌏 Add multi-language support

## Changelog

### v1.0.0 (2024-01-15)

**New Features**:

- Initial release
- Support for 20+ pip source speed tests
- Modern Web interface
- Responsive design
- Concurrent speed testing optimization
- History record saving
- Complete API interface

**Technical Improvements**:

- Frontend rebuilt with React 18
- Backend rebuilt with Flask 2.3
- TypeScript support added (optional)
- Improved error handling mechanism

**Bug Fixes**:

- Fixed inaccurate timeout detection for some sources
- Fixed concurrent speed test race conditions
- Fixed frontend localStorage caching issues

### Planned Features

- [ ] Add speed test history charts
- [ ] Support custom speed test parameters
- [ ] Add Dark Mode theme
- [ ] Support user login and history synchronization
- [ ] Add speed test result export function
- [ ] Support more overseas mirror sources
- [ ] Add Docker Compose configuration

## Disclaimer

This tool is provided for learning and research purposes only.

### Usage Restrictions

Please note the following when using this tool for speed testing:

#### 1. Network Environment Impact

Speed test results are affected by the following factors, and actual usage experience may differ from speed test results:

- Local network environment (Wi-Fi, Ethernet, 4G/5G)
- Network operator (Telecom, Unicom, Mobile, Education Network)
- Test time period (peak hours, off-peak)
- Network congestion level
- Geographic location

#### 2. Source Availability

The third-party pip sources integrated in this tool are maintained by various universities, organizations, or individuals, and the service status and availability of sources are beyond the control of this tool:

- Some sources may be unavailable at certain times
- Source addresses may change at any time
- Source service quality may change
- Some community sources may be discontinued

#### 3. Data Security

- This tool only performs HTTP HEAD requests to measure latency, and does not download or process any package files
- When using third-party sources, it is recommended to verify their security
- Avoid using pip sources from unknown sources to prevent supply chain attacks
- It is recommended to regularly verify the integrity of the sources being used

#### 4. Legal Liability

- The author is not responsible for any direct or indirect losses caused by using this tool
- This tool does not guarantee the accuracy or completeness of speed test results
- Users should independently judge which pip source to use
- Please do not use this tool for commercial purposes (unless authorized)

### Copyright Notice

The pip source names and addresses integrated in this tool are official information from their respective maintainers. If there is any infringement, please contact us for handling.

## Acknowledgements

Thanks to the following universities, organizations, and individuals for providing pip mirror services:

### Official and Commercial Mirrors

- **PyPI Official** - https://pypi.org - World's largest Python package index
- **Aliyun** - https://mirrors.aliyun.com - Mirror service provided by Alibaba
- **Tencent Cloud** - https://mirrors.cloud.tencent.com - Mirror service provided by Tencent Cloud
- **Huawei Cloud** - https://repo.huaweicloud.com - Mirror service provided by Huawei Cloud
- **Baidu** - https://mirror.baidu.com - Mirror service provided by Baidu
- **NetEase** - https://mirrors.163.com - Mirror service provided by NetEase

### University Mirrors

- **Tsinghua TUNA Association** - https://pypi.tuna.tsinghua.edu.cn - Mirror maintained by Tsinghua University students
- **University of Science and Technology of China** - https://pypi.mirrors.ustc.edu.cn - USTC Mirror Station
- **Shanghai Jiao Tong University** - https://mirror.sjtu.edu.cn - SJTU Mirror Station
- **Huazhong University of Science and Technology** - https://pypi.hust.edu.cn - HUST Mirror Station
- **Beijing Institute of Technology** - https://pypi.bit.edu.cn - BIT Mirror Station
- **Dalian University of Technology** - https://pypi.dut.edu.cn - DUT Mirror Station
- **Dalian Neusoft University of Information** - https://mirrors.neusoft.edu.cn - Neusoft Mirror Station
- **Lanzhou University** - https://pypi.lzu.edu.cn - LZU Mirror Station
- **Xidian University** - https://pypi.xidian.edu.cn - Xidian Mirror Station
- **Nanjing University** - https://pypi.nju.edu.cn - NJU Mirror Station
- **Chinese Academy of Sciences** - https://pypi.mirrors.casct.com - CAS Mirror Station
- **Zhejiang University** - https://pypi.zju.edu.cn - ZJU Mirror Station

### Community Mirrors

- **Douban** - https://pypi.doubanio.com - Community-maintained mirror
- **TU Dresden** - https://pypi.tu-dresden.de - Mirror from Technische Universität Dresden, Germany
- **BH6BHG** - https://bc9ce2eff4cc.ngrok-free.app - Community-maintained mirror by individual

### Open Source Project References

The development of this project references the following excellent projects:

- **[cnpip](https://github.com/sunny5261/cnpm)** - Python package management tool, automatically switches fastest npm mirror
- **[pypi-mirrors](https://github.com/pypi-mirrors/pypi-mirrors)** - Python PyPI mirror list
- **[python-whois](https://github.com/richard-penman/whois)** - WHOIS query tool

### Technology Stack

Thanks to the following open source projects:

- **Flask** - Python Web Framework
- **React** - UI Component Library
- **Vite** - Build Tool
- **requests** - Python HTTP Library

### Contributors

Thanks to all friends who contributed code and suggestions to this project!

## Contact

- **Project Maintainer**: BH6BHG
- **GitHub**: [https://github.com/bh6bhg/pip-speed-tester](https://github.com/bh6bhg/pip-speed-tester)
- **Issue Reporting**: [https://github.com/bh6bhg/pip-speed-tester/issues](https://github.com/bh6bhg/pip-speed-tester/issues)

## Supporting the Project

If you find this project helpful, welcome to:

- ⭐ Star this project
- 📢 Share with friends who need it
- 🐛 Report bugs or 💡 Make suggestions
- 🔧 Contribute code

---

<p align="center">
  Made with ❤️ by BH6BHG
</p>
