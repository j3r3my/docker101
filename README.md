# Docker 101

### Building a .Net Core application in Docker

```bash
# Build the container
docker build --no-cache -f dockerfile -t j3r3my/dotnettest:latest

# Ensure we're logged into Docker 
docker login

# Push to public Docker repo (update if you have your own)
docker push j3r3my/dotnettest:latest
```