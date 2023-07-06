# Issues and Bug Tracker

## Issues
- [] docker-compose keeps restarting when starting up
    + Status: Ongoing
    - Steps to recreate:
        1. Startup docker-compose: `docker-compose up -d --build`
        2. Check docker processes: `docker ps`
            + container should be restarting
    - Methods tried:
        - Tried building and running manually via docker build && docker run
            + Result: Working
    - Possible issues:
        + Something within the compose-file


