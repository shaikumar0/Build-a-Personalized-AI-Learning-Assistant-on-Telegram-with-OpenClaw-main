FROM node:lts

# Install openclaw globally
RUN npm i -g openclaw@latest || true

# Create a non-root directory for OpenClaw data
RUN mkdir -p /root/.openclaw/skills
WORKDIR /root/.openclaw

# Copy skills into image (build-time). In production, mount a volume instead.
COPY skills /root/.openclaw/skills

EXPOSE 3000

CMD ["sh", "-c", "openclaw gateway start"]
