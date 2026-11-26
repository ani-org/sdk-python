# ANI sdk-python Quick Start Guide

### 📋 Prerequisites
- Python 3.12 (Windows / Linux)
- Network access to the agent gateway server
- Python dependencies:
```bash
a2a-sdk>=1.0,<1.3
aioquic>=1.2
grpcio>=1.60
protobuf>=5.29.5
cryptography>=43.0.0
```

### Installation
1. Install Python 3.12

2. Install Python packages (enter SDK directory)
```bash
pip install -r requirements.txt
```
Slow download? Use a mirror, e,g.:
```bash
pip install -r requirements.txt -i [https://pypi.tuna.tsinghua.edu.cn/simple](https://pypi.tuna.tsinghua.edu.cn/simple)
```

3. Deploy ANI SDK `.so` libraries
```bash
SITE=$(python3.12 -c "import site; print(site.getsitepackages()[0])")
cp -f linux-x86_64/*.so "$SITE"/
cd /tmp && python3.12 -c "import ani_sdk; print('import OK')"
```
> ✅ Verify outside the `.so` directory to avoid local path loading issues.

Self-check (gateway connection not required):
```bash
python3.12 -c "
from ani_sdk import ANIRuntime, RuntimeConfig, ControlPlaneConfig, IdType, AmtpTransportConfig, AgentServer, make_agent_card
from ani_sdk.a2a_amtp import A2A_AMTP_PROTOCOL_BINDING, create_amtp_client_factory
print('Top-level API OK')"
```

4. Update ANI SDK
```bash
SITE=$(python3.12 -c "import site; print(site.getsitepackages()[0])")
cp -f linux-x86_64/*.so "$SITE"/
cd /tmp && python3.12 -c "import ani_sdk; print('import OK')"
```

### Example: Echo Demo
Navigate to the `examples` folder:
```bash
# Start agent server
python myserver.py
```
Check registration status via the gateway web UI.
```bash
# Start client
python myclient.py
```
Echo results will be printed.

### 📚 API Reference
See documentation within the SDK directory for full API details.

### 🔐 Security Notice
This is an experimental deployment. **Do not run production services on it.**
