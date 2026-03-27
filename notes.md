# Vaultwarden Build Notes

## Attempt 1
- Forgot to handle the admin token properly
- Created both an example compose file and a personal compose file
- Added the personal compose file to `.gitignore`

## Attempt 2
- Tried to start the container from VS Code
- Docker returned a permissions error
- Learned that Docker uses a Unix socket and my user did not have permission to access it

## Attempt 3
- Used `sudo docker-compose up -d --build`
- Container started successfully

## Lessons Learned
- Docker permissions matter on Linux
- YAML indentation and file structure matter
- It is better to keep secrets out of tracked files
- Reverse proxying through Nginx is safer than exposing the container directly

## VS Code Integration

- Installed Remote SSH extension
- Connected VS Code directly to Azure VM
- Opened project folder remotely
- Now able to edit files visually instead of using nano
- Using VS Code terminal for Docker and Git commands

Lesson:
Using a proper IDE significantly improves speed and readability when working with infrastructure projects.
