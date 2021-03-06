Kumu
====

Project Goal
----

Kumu CMS aspires to be the best tool for keeping track of all the information related to creative projects. It is not aimed at content creation, although it will include tools for that. It is primarily aimed at private information storage and management,   solid syncing across devices, transparent storage of files, an ability to publicly publish anything in the library, and solid automated tagging and browsing systems.


Storage Format
----

Information storage is through markdown files stored in a git repository[\[a\]](#a-jesse-anderton), with metadata stored in the file using markdown metadata tags. The file contents will be indexed for management features, but the file itself is the master copy and the indexer should pick up file changes as quickly as possible. Media files can also be stored, with metadata in an associated markdown file.


Snippets, Chrome, and Media
----

All content in the CMS is provided as Markdown text.  These files can be subdivided into three categories:

* _Snippets_ are the main data we are storing.  They can be any kind of text, URLs, images, references to published works, etc.
* _Chrome_ are files which define views for snippets.  They use special syntax to import snippets. Snippets are not directly rendered as HTML; that’s the job for chrome files.
  * We should ship with several standard views to provide the main Kumu UI.
	* We may need a special template syntax for, e.g., embedding metadata field contents into the chrome or for iterating over all matching snippets.
* _Media_ are binary data files: images, videos, etc.  They can also have associated markdown files which provide metadata tags for the files.


Repository Structure
----

A given installation of Kumu will be a git repository with the following folder structure:
* chrome: Contains markdown files related to site structure and presentation
* chrome/css: Contains CSS files included elsewhere
* chrome/js: Contains JavaScript files included elsewhere
* index: Contains files generated by the indexer as it scans markdown files for changes.  These files are used (indirectly) by chrome templates to provide a faster implementation of snippet queries.
* media: Contains media files (e.g. images) used in snippets and chrome files (possibly in a nested folder structure).  Also contains markdown files providing metadata for these media files.
* snippets[\[b\]](#b-jesse-anderton): Contains markdown files which represent the core repository content (possibly in some nested folder structure, such as YYYY-MM or YYYY/MM-DD folders)

Metadata Tags
----

The[\[c\]](#c-christopher-anderton) complete current supported metadata tags are as follows (mainly taken from here):
* Title: The title of the document
* Subtitle: The subtitle
* Author: The creator of the document
* Affiliation: The organization with whom the author created the content
* License: The license string for the document, e.g. Copyright, Creative Commons, MIT, Apache, etc.
* CSS: The stylesheet to include when rendering the document as HTML
* Date: The last modification date for the content
* Date-Created: The first modification date for the content
* Keywords: A list of comma-separated keywords for the document
	* The special keyword “starred” is used to mark a file as starred
	* Other special keywords[\[d\]](#d-jesse-anderton), such as “rss,” are used to publish files to particular services
* Access: A string indicating the document permissions: public, private, or an ACL name.  This affects the audience to whom the file will be visible and editable.

Imported Comments
----
##### [a] Jesse Anderton:
We need a more detailed discussion of this.  How does git relate to dropbox?  When will we push/pull/clone the git repository?  We should probably have a file versioning and syncing section in the document.

##### [b] Jesse Anderton:
This is opinionated: only chrome has css and js folders, not snippets.  Is that what we want?

##### [c] Christopher Anderton:
Should we include RDF triples and/or linked open data?

##### [d] Jesse Anderton:
Is this sufficient to control publication to services?  Pro: we just use keywords for querying the files this service wants.  Con: we might not want to mix keywords-about-content and keywords-about-publication.

##### [e] Jesse Anderton:
I have struck through things which I think are covered above.  I think the organizational style used above provides a clearer explanation and neater segmentation into distinct topics.  If you happen to agree, then let’s organize the document like that and make sure all the information below is put into an appropriate section.

##### [f] Jesse Anderton:
Sounds like a UI-and-service  implementation detail.  We'll need to talk client-side and server-side stuff to flesh this kind of thing out -- so far it's just file storage and format stuff.

##### [g] Jesse Anderton:
I'd also love to see BibTeX support.  And, for that matter, LaTeX math rendering, which MultiMarkdown already supports.  This would make the tool much more useful for use as a research aid.

