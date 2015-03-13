[SourceForge](http://sourceforge.net/) has been hosting open-source software since 1999, and boasts over [400,000 projects](http://sourceforge.net/about). This document will cover how to migrate a project from Google Code to SourceForge, which supports the SVN, Git, and Mercurial version control systems.

The migration will be done using SourceForge's [Google Code Project Importer](https://sourceforge.net/p/import_project/google-code/).

# Sign in to SourceForge #
If you do not already have a SourceForge account, create one and log in.

# Navigate to the Importer Tool #
Navigate to the easy-to-use Google Code Project Importer:
https://sourceforge.net/p/import_project/google-code/

This tool will import your project’s wikis, issues, existing downloads, and, of course, your project’s source code. You can learn more specifics by reading the tool’s [documentation](http://sourceforge.net/p/forge/documentation/Google%20Code%20Importer/).

You do not need to create a new SourceForge project before importing your Google Code project; when you start the importer tool, the SourceForge project will be created for you.

Once you click Import, the process will start. You will get emails as various import steps complete, such as when all the wiki pages have been migrated.

# URL Redirection #
Once a project has been successfully exported to SourceForge, you will want to update your project's homepage on Google Code to avoid confusion.

Some project owners simply update their project homepage's text to indicate it has moved. For example [subtext](http://code.google.com/p/subtext) or [bwapi](http://code.google.com/p/bwapi).

Another option is to set the Google Code "project moved" flag. When set, attempts to access the project will take users to an interstitial page indicating the new project location. In the future, the page will automatically redirect your new project on sourceforce.net.

To set the "project moved" flag, navigate to your project's advanced admin page, at https://code.google.com/p/project-name/adminAdvanced.

Once there, enter the new project home page URL under "project moved". For example: https://sourceforge.net/p/fuego. Finally click the "Project Moved" button.