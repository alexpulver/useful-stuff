# Useful stuff

> Don’t look for a great Idea, find a good Problem to solve.

> Drawing architecture diagrams makes unclear things clear and clear things obvious

> AWS CDK allows you to code the application's architecture and logic side by side in the same language

### Remove all packages installed by pip
```bash
pip uninstall -y -r <(pip freeze)
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
