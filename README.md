# Jetson local VLM demo

This folder contains the Live VLM WebUI checkout, the Docker Compose setup, and the Hugging Face/runtime caches for Gemma 4 E2B.

## Open the demo

On the Jetson desktop, open `http://localhost:8090`, allow camera access, select the USB webcam, then start camera analysis. The browser UI and inference API bind to loopback only; the backend API is `http://localhost:8000/v1`.

## Manage the containers

```bash
cd "/home/algosium/jetson vlm"
docker compose ps
docker compose logs -f gemma4-e2b
docker compose down
docker compose up -d
```

`docker compose down` keeps the model and runtime caches. Model downloads are stored in `cache/huggingface`; vLLM compile caches are stored in `cache/vllm` and related cache folders. The Live VLM WebUI source is in `live-vlm-webui`.

Docker stores pulled container image layers in its configured system image store, outside this project folder. The actual model weights and project files are inside this folder.

The model is Gemma 4 E2B in BF16. The Compose configuration limits context to 8,192 tokens, one active sequence, and 40% GPU memory utilization to leave resources for the desktop.
