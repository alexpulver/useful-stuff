# Useful stuff

### Mindset sentences
> Don’t look for a great Idea, find a good Problem to solve (Someone)

> Abstraction in the cloud: a *service* with higher-level vocabulary that shields from the complexity, security and operations of the underlying implementation (Alex Pulver)

> Infrastructure libraries provide compositions, not abstractions, because consumers own security and operations of the underlying implementation (Alex Pulver)

> Drawing architecture diagrams makes unclear things clear and clear things obvious (Alex Pulver)

> A system is only evolvable if you can easily understand it and you can safely change it ([Rebecca Parsons](https://www.infoq.com/podcasts/evolutionary-architecture-evolution/))

> AWS CDK allows you to code the application's architecture and logic side by side in the same language (Alex Pulver)

### Web application OIDC authentication flow approach
Client-side design:
* Store refresh token as HTTP-only secure cookie
* Store ID token in memory

Client/server flow:
* Client sends POST request to `/auth/refresh` API
* If user didn't authenticate yet, client gets `401` response (there is no refresh token cookie), and redirects to `/auth/login` API
  * After user authenticates, `/auth/login` API sets refresh token cookie, and responds with ID token
* Client calls APIs with ID token in Authorization header
* APIs authenticate calls using ID token

Related information:
* [How to Persist JWT Tokens for Your SaaS Application](https://frontegg.com/guides/how-to-persist-jwt-tokens-for-your-saas-application)

### Remove all packages installed by pip
```bash
pip uninstall -y -r <(pip freeze)
```

### List licenses of Python packages installed with pip
```bash
pipx install pip-licenses
pip-licenses --python /usr/bin/python -nv --output-file licenses.txt
```

### Resolve packaging dependency version conflict between black and safety
```bash
pip-compile -P black==22.12.0 --upgrade requirements-dev.in
```

### Bash command to perform an operation on multiple AWS CloudFormation stacks
```bash
for stack in $(aws cloudformation describe-stacks --query Stacks[].StackName --output text); do echo $stack; done
```

### List physical resource IDs of specific resource types in an AWS CloudFormation stack
```bash
aws cloudformation list-stack-resources --stack-name STACK_NAME --query 'StackResourceSummaries[?ResourceType==`RESOURCE_TYPE`].PhysicalResourceId'
```

### `cfn_nag` command for `cdk.out` directory
```bash
cfn_nag_scan --output-format txt --input-path cdk.out/ --template-pattern '..*\.template\.json'
```

### PyCharm external documentation for AWS CDK
PyCharm => Preferences => Tools => [External documentation](https://www.jetbrains.com/help/pycharm/viewing-reference-information.html#external-docs) => Module Name: `aws_cdk` => URL/Path Pattern: `https://docs.aws.amazon.com/cdk/api/v2/python/{module.name}/{class.name}.html`

### `tree` command for AWS CDK project
```bash
tree --dirsfirst --matchdirs -I '.mypy_cache|cdk.out|node_modules|__pycache__|.git|.idea'
```

### `history` without numbers
```bash
history -w /dev/stdout
```

### Disable AWS Cloud9 managed temporary credentials
```bash
aws cloud9 update-environment  --environment-id $C9_PID --managed-credentials-action DISABLE
rm -vf ${HOME}/.aws/credentials
```

### Archive, tree and diff two projects directories
Archive
```bash
git archive --prefix=aws-cdk-project-structure-python/ -o aws-cdk-project-structure-python.zip HEAD
```

Tree
```bash
$ fd | as-tree
```

Diff two AWS CDK project trees
```bash
diff -qrub -x "cdk.out" -x "node_modules" -x ".git" -x "package-lock.json" -x "chalice.out" -x "__pycache__" -x ".idea" -x ".chalice" -x ".DS_Store" -x ".mypy_cache" aws-cdk-sam-chalice/ aws-cdk-project-structure-python/
```

### Replace AWS CDK version in requirements file
```bash
sed -i .orig 's/1\.106\.1/1\.114\.0/g' requirements.txt
```

### Make `bash` case-insensitive for the current user
```bash
# If ~/.inputrc doesn't exist yet: First include the original /etc/inputrc
# so it won't get overriden
if [ ! -a ~/.inputrc ]; then echo '$include /etc/inputrc' > ~/.inputrc; fi

# Add shell-option to ~/.inputrc to enable case-insensitive tab completion
echo 'set completion-ignore-case On' >> ~/.inputrc
```

### Google Chrome deep linking
`#:~:text=`

### Stop iTunes from launching when connecting Bluetooth devices
https://www.howtogeek.com/274345/stop-itunes-from-launching-when-you-press-play-on-your-macs-keyboard/
+
https://stackoverflow.com/questions/6442364/running-script-upon-login-mac

### pyenv plugins
[pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv) - manage virtualenvs and conda environments

### Pretty print raw JSON string
```bash
aws cloudtrail lookup-events --max-results 1 --query 'Events[0].CloudTrailEvent' | jq 'fromjson'
```

### Restart macOS sound driver
```bash
sudo pkill coreaudiod
```

### Outlook query for tasks in calendar
`category:="Israel Israeli" OR category:="Israel Israelit" start:>=today isrecurring:no`

### Simple HTTP request handler
```bash
python -m SimpleHTTPServer 8000
```

### Change macOS font smoothing
```bash
defaults -currentHost write -g AppleFontSmoothing -int [0,1,2,3]
``` 
and restart

### System design examples
* URL shortener or TinyURL: https://lnkd.in/gJPWZsX3
* Social media app like Twitter: https://lnkd.in/guParNhY
* File sharing service like Dropbox: https://lnkd.in/gnSQ6rAd
* Video streaming service like Netflix: https://lnkd.in/gnHSyCj8
* Autocomplete feature of Google: https://lnkd.in/g3VFcaYN
* Messaging app like WhatsApp: https://lnkd.in/g5zJa_4W
* Online document editor like Google docs: https://lnkd.in/gBvztEqV
* Proximity service like Uber: https://lnkd.in/grtPbr6k
* Hotel booking service like Airbnb: https://lnkd.in/gWjrGwCM
* Web crawler: https://lnkd.in/gTkfCH8U
