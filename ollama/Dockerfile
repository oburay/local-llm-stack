FROM ollama/ollama:latest

# Expose the port for the server
EXPOSE 11434

# Create a startup script that checks if model exists before downloading
RUN echo '#!/bin/sh\n\
MODEL_PATH="/root/.ollama/models/manifests/registry.ollama.ai/library/deepseek-r1/latest"\n\
if [ ! -f "$MODEL_PATH" ]; then\n\
  echo "Model not found, downloading..."\n\
  ollama serve & SERVER_PID=$!\n\
  sleep 5\n\
  ollama pull deepseek-r1:latest\n\
  kill $SERVER_PID\n\
  wait $SERVER_PID\n\
  echo "Model downloaded successfully"\n\
fi\n\
echo "Starting Ollama server..."\n\
exec ollama serve\n' > /startup.sh && chmod +x /startup.sh

# Use the startup script as the entrypoint
ENTRYPOINT ["/startup.sh"]
