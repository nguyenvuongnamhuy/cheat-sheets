# Table of Contents

- [Git](#git)
  - [Install](https://linuxconfig.org/install-git-in-linux-redhat-8)
  - [Set author identity](#set-author-identity)
  - [Show changes in untracked file](#show-changes-in-untracked-file)
  - [Remove & delete all changes](#remove--delete-all-changes)
  - [Cherry-pick commit](#cherry-pick-commit)
- [Gitlab Runner](#gitlab-runner)
  - [Install](#install)
    - [With repository](#with-gitlab-repositories--tutorial--install)
    - [With docker](#with-docker--tutorial)
  - [Commands](#commands)
- [Use multiple account](#use-multiple-accounts-in-one-machine)

# Git

## Set author identity

Insert into .git/config

```bash
[user]
  name=${USERNAME}
  email=${EMAIL}
```

## Show changes in untracked file

```bash
git diff /path-of-file
```

## Remove & delete all changes

```bash
git clean -d -f
```

## Cherry-pick commit

```bash
git cherry-pick ${COMMIT_ID}
git cherry-pick -m 1 ${COMMIT_ID}
```

# Gitlab Runner

## Install

### With GitLab repositories ( [Tutorial](https://www.youtube.com/watch?v=G8ZONHOTAQk&ab_channel=ValentinDespa) / [Install](https://docs.gitlab.com/runner/install/linux-repository.html) )

### With docker ( [Tutorial](https://www.youtube.com/watch?v=JLdPiq0owUM&ab_channel=Raaviblog) )

1. Create volume in docker

```bash
docker volume create gitlab-runner-config
```

2. Start the GitLab Runner by mounting the docker volume created before,
   after the installation is done, run `docker ps` to check if the containers exists or not

```bash
docker run -d --name gitlab-runner --restart always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v gitlab-runner-config:/etc/gitlab-runner \
    gitlab/gitlab-runner:latest
```

3. Find Gitlab Runner instance url

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ${CONTAINER_ID_GITLAB}
```

4. Register a runner

```bash
docker run --rm -it -v gitlab-runner-config:/etc/gitlab-runner gitlab/gitlab-runner register
```

Input information

```bash
Gitlab instance URL: "http://${IP}:80"

Registration token: get on Settings > CI/CD > Runners

Tags: docker (Edit or untick option "Run untagged jobs" on Settings > CI/CD > Runners > Edit runner)
```

5. Restart gitlab runner container

```bash
docker restart gitlab-runner
```

## Commands

Listing all runners

```bash
docker exec -it gitlab-runner gitlab-runner list
```

Unregister runner

```bash
docker exec -it gitlab-runner gitlab-runner unregister --name ${RUNNER_ID}
```

Remove unverified runners

```bash
docker exec -it gitlab-runner gitlab-runner verify --delete
```

Start runners

```bash
docker exec -it gitlab-runner gitlab-runner start
```

Restart runners

```bash
docker exec -it gitlab-runner gitlab-runner restart
```

Stop runners

```bash
docker exec -it gitlab-runner gitlab-runner stop
```

Gitlab Runner Configuration

```bash
cat /etc/gitlab-runner/config.toml
```

Or

```bash
cat /srv/gitlab-runner/config/config.toml
```

# Use multiple accounts in one machine

1. Edit config file (~/.ssh/config)

```bash
Host github_1
  HostName github.com
  User git
  IdentityFile ~/.ssh/private_key_1

Host github_2
  HostName github.com
  User git
  IdentityFile ~/.ssh/private_key_2
```

2. Add ssh private keys to agent

```bash
ssh-add ~/.ssh/private_key_1
ssh-add ~/.ssh/private_key_2
```

3. Test connection

```bash
ssh-keyscan github.com >> ~/.ssh/known_hosts
ssh -T git@github_1
ssh -T git@github_2
```

---
