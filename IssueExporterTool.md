If you are migrating a project to Bitbucket or GitHub, the Issue Exporter tool can help you migrate your Google Code issue tracker items to your project’s new home.

# Install Python #
First you need to [install Python](https://www.python.org/downloads/), though it should be already installed on most Mac and Linux machines.

Next, [clone the support-tools Google Code project](https://code.google.com/p/support-tools/source/checkout) (i.e. _this_ project's source code).

```
git clone https://code.google.com/p/support-tools/
```

# Use Google Takeout to Get Issue Data #
With the Python runtime installed, next we need to download a dump of all of your project's issues. To create an archive of all of your Google Code projects' issues, head to Google Takeout:
https://www.google.com/settings/takeout

Google Takeout allows you to export project data from many Google Services, but for now we are only interested in "Google Code Project Hosting".

Google Takeout will create an archive of all of your project’s issues. Note that this is only available for projects which you are an owner of. You will not be able to use Google Takeout to export archives of issues for other open-source projects.

Depending on the number of Google Code projects you own, and the number of issues they have, exporting an archive may take a very long time. Google Takeout will notify you when your archive is ready.

Once you have your issue archive, extract the file named `GoogleCodeProjectHosting.json`. This is a JSON dump of all of your projects' issues. (The issues for multiple Google Code projects will be stored in that single file.)

We will then run a few scripts on this data dump to upload your issues to another location. There are instructions are different for exporting issues to GitHub or Bitbucket.

# Exporting to GitHub #
Next we will run a script, `github_issue_convert.py`, to upload your project’s issues to a GitHub project.

## Personal Access Token ##
The next step is to create a personal access token. This is a special password that you will use for this process. When the migration is complete, you can revoke this password.

Create a personal access token by visting https://github.com/settings/applications and create a new "Personal Access Token". Be sure to check the "public\_repo" scope. (Which authorizes this access token to modify your public repos.)

## Running the Script ##
You are now all set to migrate your issues to GitHub.

The script has several parameters:
```
    usage: github_issue_converter.py 
               [-h]
               --github_oauth_token GITHUB_OAUTH_TOKEN
               --github_owner_username GITHUB_OWNER_USERNAME
               --github_repo_name GITHUB_REPO_NAME
               --issue_file_path ISSUE_FILE_PATH
               --project_name PROJECT_NAME
```

The parameters are as follows:

  * `github_owner_username` is the name of the GitHub repo owner, i.e. you. (e.g. “chrsmith”)
  * `github_oauth_token` this is the access token you generated above.
  * `github_repo_name` is the name of the repository you will be importing the issues into.
  * `issue_file_path` is the file path to your GoogleCodeProjectHosting.json file.
  * `project_name` is the name of the Google Code project whose issues you are exporting. For example "support-tools".

To run the conversion script, run the following:
```
python \
    googlecode-issues-exporter/github_issue_converter.py \
    --github_oauth_token="$GH_ACCESS_TOKEN" \
    --github_owner_username=<your-github-user-name> \
    --github_repo_name=<your-github-repo-name> \
    --issue_file_path=<your GoogleCodeProjectHosting.json file> \
    --project_name=<your-google-code-project-name>
```

### Speeding Things Up ###
Exporting issues and comments to GitHub will be _very, very_ slow. This is because the script is designed to send requests slow enough to not run afoul of GitHub's anti-abuse rate limiting.

You can get the anti-abuse rate limited for your account by [contacting GitHub](https://github.com/contact?form%5Bsubject%5D=Google+Code+Export:+API+Abuse+Rate+Limits). If you get the rate limit raised for your account, add a `--rate_limit=false` flag to the GitHub issue converter.

For more information please see the GitHub APIs [section on rate-limiting](https://developer.github.com/v3/#rate-limiting), and search for "Abuse Rate Limits".

# Exporting to Bitbucket #
Exporting issue data to Bitbucket is slightly different. Rather than using an API to export issues individually, Bitbucket takes a single archive and will process all issues at once.

We will run a script, `bitbucket_issue_convert.py`, to convert your Google Code issues dump into a format that can be imported into Bitbucket.

The Bitbucket script is very similar to the GitHub import script above.

```
python googlecode-issues-exporter/bitbucket_issue_converter.py \
    --issue_file_path=<your GoogleCodeProjectHosting.json file> \
    --project_name=<your project name> \
    --default_owner_username=<your Bitbucket username>
```

This will generate the file named `db-1.0.json`, which contains your project’s issues and comments in a format that Bitbucket can ingest.

Next you need to convert it to a zip file:

```
zip -r bitbucket-issues.zip db-1.0.json
```

## Upload the Bitbucket Issue Dump ##
Open up your project on Bitbucket, and on the "Settings" page head to "Import & Export" under "Issues".

Select `bitbucket-issues.zip` file and click "Start import". Done! Now you should have all of your Google Code issues in Bitbucket.