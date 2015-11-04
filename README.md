### SSH-Agentの設定
1. public key を経由する全てのサーバに置く
2. 対応するsecret key をローカルに置く
3. ローカルPCで
```
$eval ¥`ssh-agent¥`
$ssh-add 秘密鍵
```

### この内容の自動化は.bashrcに

```
SSH_AGENT_FILE="$HOME/.ssh/ssh-agent-info"
test -f $SSH_AGENT_FILE && source $SSH_AGENT_FILE
if ! ssh-add -l >& /dev/null ; then
  ssh-agent > $SSH_AGENT_FILE
  source $SSH_AGENT_FILE
  ssh-add
fi
```

を記入

### SSHのコンフィグファイル例

```
Host goal-pc
    HostName *.*.*.*
    Identityfile ~/.ssh/id_rsa
    Port 22
    User ***
    ProxyCommand ssh arakawa -W %h:%p

Host via-pc
    HostName *.*.*.*
    Identityfile ~/.ssh/id_rsa
    Port 22
    User ***
```
