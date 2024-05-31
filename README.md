# JENKINS

Jenkins in itself have very limited functionality. But it can become very powerful by the use of plugins.

# Role Based Authentication - Users

1. Role-based Authorization Strategy - Install this plugin which will allow to add different user groups - admin, user etc. And we can control the permissions available to a particular group.

# Delete Workspace before build start

We can select this option under build job -> Configure -> Build Environment -> Delete workspace before build starts. Click Apply -> Save

This option is useful when you try to build from a remote repo or github repo directly using a powershell script. In that case, we need to remove the previous build files, otherwise we will get an error.

# Github Repo linking with the pipeline

We can configure our build pipeline to automatically pull code from a remote repository.

Select job -> Configure -> Source Code Management -> Git(Incase of git repo) -> Repositories(add https link of the repo). Click Apply -> Save.

# Generate URL to trigger builds Remotely (from other scripts)

Select job -> Configure -> Build Triggers -> Trigger builds remotely (e.g., from scripts)(check this option) -> Fill Authentication Token.

Use the following URL to trigger build remotely: JENKINS_URL/job/demo-fourth/build?token=TOKEN_NAME or /buildWithParameters?token=TOKEN_NAME
Optionally append &cause=Cause+Text to provide text that will be included in the recorded build cause.

This will only only work when user is logged in into jenkins and not work when you call this using shell script which will execute from the remote machine terminal.

# Trigger Build Remotely without worrying about login creds

Install Plugin -> Build Authorization Token Root Plugin

After installing use this url pattern to trigger build remotely:
JENKINS_URL/buildByToken/build?job=NAME&token=SECRET or
read this documentation if you want to use parameters: https://plugins.jenkins.io/build-token-root/

Since '&' is a special character, we need to use '\' before this while using inside shell scripts.
eg: http://localhost:8080/buildByToken/build?job=demo-fourth\&token=mysecrettoken

# Build after other projects are built

Use this option, when you want to automatically trigger your build job when some other job completes successfully. You can access this option from job -> Configure -> Build Triggers -> Build after other projects are built -> Enter the job name you want to configure. Click Apply -> Save.

# Run a job periodically - Like every 2 mins

Go to Configure --> Build Periodically --> Give a cron schedule to run job periodically.
