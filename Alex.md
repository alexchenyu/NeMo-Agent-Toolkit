00 toolkit overview
```bash
git clone git@github.com:NVIDIA/NeMo-Agent-Toolkit.git
cd NeMo-Agent-Toolkit
git submodule update --init --recursive

# 安装 Git LFS
sudo apt update
sudo apt install git-lfs -y
git lfs install
git lfs fetch
git lfs pull


curl -Ls https://astral.sh/uv/install.sh | bash
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
uv self update
uv venv --seed .venv
source .venv/bin/activate
uv sync --all-groups --all-extras
nat --version

uv pip install -e examples/frameworks/multi_frameworks
export NVIDIA_API_KEY=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
nat run --config_file=examples/frameworks/multi_frameworks/src/nat_multi_frameworks/configs/config.yml --input "tell me about this workflow"

export TAVILY_API_KEY=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
nat run --config_file=examples/frameworks/multi_frameworks/src/nat_multi_frameworks/configs/config.yml --input "what is Compound AI?"

nat serve --config_file=examples/frameworks/multi_frameworks/src/nat_multi_frameworks/configs/config.yml --host 0.0.0.0 --port 8000
curl -X 'POST' \
'http://localhost:8000/generate' \
-H 'accept: application/json' \
-H 'Content-Type: application/json' \
-d '{"input_message": "What is Compound AI?"}'


cd external/nat-ui
sudo apt udpate
sudo apt install -y nodejs
npm install
# export PORT=7788
npm run dev

# launch http://localhost:3000

# add content in: examples/frameworks/multi_frameworks/src/nat_multi_frameworks/configs/config.yml
general:
  use_uvloop: true
  telemetry:
    logging:
      console:
        _type: console
        level: WARN
      file:
        _type: file
        path: /tmp/multi_frameworks.log
        level: DEBUG
    tracing:
      phoenix:
        _type: phoenix
        endpoint: http://localhost:6006/v1/traces
        project: multi_frameworks

uv pip install arize-phoenix
phoenix serve
nat run --config_file=examples/frameworks/multi_frameworks/src/nat_multi_frameworks/configs/config.yml --input "tell me about this workflow"
# Navigate to http://localhost:6006/ in your browser to view the details of the tracing of this workflow.

nat run --config_file=examples/frameworks/multi_frameworks/src/nat_multi_frameworks/configs/config.yml --input "what is Compound AI?"
```

01 new workflow_car maintenance
```bash
nat workflow create --workflow-dir examples car_maintenance

# examples/car_maintenance/pyproject.toml
dependencies = [
  "nvidia-nat[llama-index,langchain]~=1.2",
  "faiss-cpu==1.8.0.post1",
  "llama-index-vector-stores-faiss==0.3.0",
  "colorama~=0.4.6"
]

```
