# Useful commands, links and queries

### `cfn_nag` command for `cdk.out` directory
```
cfn_nag_scan --output-format txt --input-path cdk.out/ --template-pattern '..*\.template\.json'
```

### PyCharm external documentation for AWS CDK
PyCharm [External documentation](https://www.jetbrains.com/help/pycharm/viewing-reference-information.html#external-docs) => Module Name: `aws_cdk` => URL/Path Pattern: [`https://docs.aws.amazon.com/cdk/api/latest/python/{module.name}/{class.name}.html#{module.name}.{class.name}`](https://docs.aws.amazon.com/cdk/api/latest/python/%7Bmodule.name%7D/%7Bclass.name%7D.html#{module.name}.{class.name)

### `history` without numbers
```
history -w /dev/stdout
```

### Disable AWS Cloud9 managed temporary credentials
```
aws cloud9 update-environment  --environment-id $C9_PID --managed-credentials-action DISABLE
rm -vf ${HOME}/.aws/credentials
```

### Archive, tree and diff two projects directories
Archive
```
git archive --prefix=aws-cdk-project-structure-python/ -o aws-cdk-project-structure-python.zip HEAD
```

Tree
```
$ fd | as-tree
```

Diff two AWS CDK project trees
```
diff -qrub -x "cdk.out" -x "node_modules" -x ".git" -x "package-lock.json" -x "chalice.out" -x "__pycache__" -x ".idea" -x ".chalice" -x ".DS_Store" -x ".mypy_cache" aws-cdk-sam-chalice/ aws-cdk-project-structure-python/
```

### Replace AWS CDK version in requirements file
```
sed -i .orig 's/1\.106\.1/1\.114\.0/g' requirements.txt
```

### Make `bash` case-insensitive for the current user
```
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
`aws cloudtrail lookup-events --max-results 1 --query 'Events[0].CloudTrailEvent' | jq 'fromjson'`

### Restart macOS sound driver
`sudo pkill coreaudiod`

### Outlook query for tasks in calendar
`category:="Israel Israeli" OR category:="Israel Israelit" start:>=today isrecurring:no`

### Simple HTTP request handler
`python -m SimpleHTTPServer 8000`
