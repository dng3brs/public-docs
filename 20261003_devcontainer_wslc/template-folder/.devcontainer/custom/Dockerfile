個人固有の情報をコンテナイメージに反映するDockerfileです。
必ず編集してからビルドしてください。（この説明2行は削除しないとエラーになります）

FROM base-for-devcontainer:latest

RUN git config --global user.email xxx@yyy.zzz \
 && git config --global user.name xxx \
 && curl -fsSL https://chatgpt.com/codex/install.sh | sh \
 && bash -c 'echo "sandbox_mode = \"danger-full-access\"" >> ~/.codex/config.toml' \
 && bash -c 'echo "approval_policy = \"on-request\"" >> ~/.codex/config.toml' \
 && bash -c 'echo "machine github.com" > ~/.codex/config.toml' \
 && bash -c 'echo "machine github.com" > ~/.netrc' \
 && bash -c 'echo "login dng3brs" >> ~/.netrc' \
 && bash -c 'echo "password ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx" >> ~/.netrc'

WORKDIR /workspaces
