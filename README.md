# dockercoins

```
github_username=lauraherreros
github_repo=dockercoins
github_branch=2021-09

git clone https://github.com/${github_username}/${github_repo}
cd ${github_repo}/
git checkout ${github_branch}

for app in hasher rng webui worker
do
  docker image build --file Dockerfile-${app} --tag ${github_username}/${github_repo}:${github_branch}-${app} /mnt/
done

docker container run --entrypoint ruby --rm --volume ${PWD}/hasher/hasher.rb:/app/hasher.rb:ro --workdir /app/ ${github_username}/${github_repo}:${github_branch}-hasher hasher.rb

docker container run --entrypoint python --rm --volume ${PWD}/rng/rng.py:/app/rng.py:ro --workdir /app/ ${github_username}/${github_repo}:${github_branch}-rng rng.py

docker container run --entrypoint node --rm --volume ${PWD}/webui/webui.js:/app/webui.js:ro --volume ${PWD}/webui/files/:/app/files/:ro --workdir /app/ ${github_username}/${github_repo}:${github_branch}-webui webui.js

```
