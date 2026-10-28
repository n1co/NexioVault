# DL du modele
ollama run qwen3-coder:30b

export ANTHROPIC_BASE_URL="http://localhost:11434"
export ANTHROPIC_AUTH_TOKEN="ollama"
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1:

claude --model qwen3-coder:30b