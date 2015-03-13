If you have a question that isn't answered here, please log an issue in the [issue tracker](https://code.google.com/p/support-tools/issues/list) or [contact Google](mailto:google-code-shutdown@google.com) for assistance.



# Questions #

## Where did my Google Code wikis go? ##
The wikis of projects exported to GitHub are converted into Markdown and placed in new `wiki` branch in the GitHub project's repo.

## How can I export private issues? ##
Issues on Google Code can be labeled in such a way that they are private (e.g. those with `Restrict-View-*`). Private issues will be migrated to GitHub as if they were deleted. None of their contents will be migrated.

If you need to export private issues, you should not use the Google Code Exporter, and instead [manually export](https://code.google.com/p/support-tools/wiki/MigratingToGitHub) your project to GitHub.

As part of that process, you will use Google Takeout to get a full archive of your projects issues, which includes those marked as restricted. And the [Issue Exporter](https://code.google.com/p/support-tools/wiki/IssueExporterTool) tool will allow you to import them to GitHub.

## Are all projects available to be exported to GitHub? ##
No. Some projects are blocked from automatic export to GitHub, specifically those that have too many issues (1,000+) or those which have already moved.

In these situations, you will need to [manually export](https://code.google.com/p/support-tools/wiki/MigratingToGitHub) your project to GitHub.

## Can I migrate a Google Code repository to a GitHub Organization? ##
No, however you can quickly transfer the repository after the export is complete.

For more information about transferring a repository on GitHub, see [this document](https://help.github.com/articles/transferring-a-repository/).

# Setting the "Project Moved" Flag #

Once a project has been successfully exported to GitHub, you will want to update your project's homepage on Google Code to avoid confusion.

Some project owners simply update their project homepage's text to indicate it has moved to GitHub. For example [subtext](https://code.google.com/p/subtext/) or [bwapi](https://code.google.com/p/bwapi/).

Another option is to set the Google Code "project moved" flag. When set, attempts to access the project will take users to an interstitial page indicating the new project location. In the future, the page will automatically redirect to well-known project hosting services such as [github.com](https://github.com).

To set the "project moved" flag, navigate to your project's advanced admin page, at https://code.google.com/p/project-name/adminAdvanced.

Once there, enter the new project home page URL under "project moved". For example: https://github.com/google/kythe. Finally click the "Project Moved" button.

# Known Issues #

This section covers a few common errors you might run into. If you encounter any other bugs or unexpected conversion issues, please log issues in the [issue tracker](https://code.google.com/p/support-tools/issues/list).

## Error "GitHub code import took too long." ##

If the GitHub import process takes too long the project export is terminated. Please retry your project export, and if the problem persists contact [Google](mailto:google-code-shutdown@google.com) or [GitHub](https://github.com/contact?form%5Bsubject%5D=Google+Code+Export:+Error+code+import+took+too+long).

## Error "Project cannot be migrated because it has too many issues." ##
There is a hard limit on the number of issues that can be exported by the tool, per repo. If your project has more than 1,000 issues the export will fail.

To migrate your issues repos, you will need to use the stand-alone [Issue Exporter](https://code.google.com/p/support-tools/wiki/IssueExporterTool).

## Error "Error migrating issues." ##

There was an error migrating your projects issues. You can try re-exporting your project in GitHub (deleting the repo, and then using the Exporter tool again).

If the problem persists, please report it in the [issue tracker](https://code.google.com/p/support-tools/issues/list). Be sure to include the name of the Google Code project you are trying to export.

## Error "Internal Server Error." ##

Aw snap! Sometimes gremlins work their way into the system. We do our best to stamp them out, but with Google's free food it is hard to avoid snacking after midnight...

If you see this error someone will be looking into it. Wait a while and retry your project export again.

## Error "GitHub code import failure." ##

This error occurs when the GitHub code import API fails. Usually this issue is transient. But if it persists, contact Google or GitHub.

## Error "Project already exists." ##

Projects will be migrated to GitHub creating a repo with the same name as the Google Code project. It is not possible to specify a different name for the GitHub repo.

If your GitHub account already has a repo with the name of the project you wish to export, you will be prohibited from migrating that project from Google Code.

To work around this, you can temporarily rename your GitHub repo by going to the repo's settings.