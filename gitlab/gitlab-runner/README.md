# How to register
1) Enter the container
```shell
docker exec -it gitlab-runner bash
```
2) Run the setup
```
gitlab-runner register
```
3) Get the token from the gitlab ui for group, project, instance. Whatever level you require.
4) Enter the following in the prompts
```shell
# Enter the GitLab instance URL (for example, https://gitlab.com/):
https://gitlab.example.com       # your url
# Enter the registration token:
GR13123213132321r8F7             # token 
# Enter a description for the runner:
misp runner 2                    # desc ( optional )
# Enter tags for the runner (comma-separated):
first                            # tags ( optional )
# Enter optional maintenance note for the runner:
no idea                          # note ( optional )
# Enter the default Docker image (for example, ruby:3.3):
# if the user doesn't specify their docker image it will use this image
# user should do image: nginx:latest otherwise fall back to :
alpine:latest
```

# Troubleshooting
Place the gitlab host's public cert in /gitlab-runner/config/certs/ so the runner can trust the gitlab server.
