.. header:: 

    .. raw:: html

	<h1 class="title">Attachments Documentation</h1>

.. class:: version

**Version 2.2-RC2 - January 16, 2011**

.. contents::
    :depth: 1


Introduction
============

The 'Attachments' extension for Joomla! allows files to be uploaded
and attached to articles or other types of content. 'Attachments' includes a
plugin to display the attachments and a component for uploading and managing
attachments. There are options to control who can see the attachments and
who can upload them, along with several other options to increase its
flexibility and usefulness. Note: all options are controlled through the
component manager. 

.. warning:: The *Attachments* extension only works for Joomla! 1.5.  
             It has not been ported to version 1.6.**

The 'Attachments' extension has been translated into many different
languages.  Please see the `Translations`_ section for the list of
available translations.  Most of these languages packs are in the process
of being updated for 'Attachments' version 2.0.

If you wish to subscribe to an email list for announcements about
this extension, please subscribe using this web page:

* `Attachments Email List ( http://jmcameron.net/attachments/email-list.html )
  <http://jmcameron.net/attachments/email-list.html>`_


New features in Version 2.0
===========================

* You can now manage attachments from the article editor, including adding,
  editing, and deleting attachments.
* All attachments are updated by Ajax and do not require full page reloads.
* You can "attach" URLs as well as files to content items.
* You can show the attachments list anywhere in an article (or content item).
* New optional field in attachments lists to display the name of the uploader
* Implemented a multi-installer so that installation of all parts of the
  'Attachments' extension only requires one install (and enables the plugins
  automatically).  This makes it extremely easy to install this extension
  even though it now has one component and seven plugins.  Note that the
  Joomla! 'upgrade' method is now the default for all parts of the
  'Attachments' extension.  This means that you do not need to UN-install old
  versions of 'Attachments' before installing this version.
* Converted attachment file storage to use paths like::

        attachments/article/23/file.txt

  This eliminates all file prefixes used in earlier versions.  It does
  mean that any one content item cannot have duplicate file names.  This
  is not much of a limitation in practice.
* Refactored the code to add "Attachments plugins".  These plugins allow
  attaching files to any content item that invokes the ``onPrepareContent``
  plugin.  For example, you can now attach files to Section and Category
  descriptions.  With a bit of work, an extension developer can create a
  new 'Attachments' plugin to support adding attachments to things like CB
  personal info displays, Virtuemart product descriptions, etc.  See
  section `What Can Files Be Attached To?`_ for more details.  
* In the administrative back end:
     - It is now possible to add attachments to articles while they are
       being created! 
     - There is an option to suppress listing attachments to unpublished
       or trashed articles or content items (although there is an easy
       way to see them if you wish).
     - Added filtering to the list of articles
     - Reworked the tabular listing in the back end to allow sorting on
       various columns
     - Several new administrative utility commands
* Improved Unicode handling in filenames
* Added more flexibility to "Who can see" and "Who can update" options.
* Added code to fix CSS problems when the Joomla! installation is using
  caching. 

Uploading Restrictions
======================

Not all types of attachment files can be uploaded.  The 'Attachments' extension
will not allow uploading of files that are not permitted by the Joomla! Media Manager.
To see (or change) what file types are allowed, go to the **Global Configuration**
page and click on the **System** tab.  In the *Media Settings* area, there are
options for controlling what types of file extensions and mime types are permitted
for uploads. The 'Attachments' extension respects these limitations.  However, the
restriction on 'Legal Image Extensions (File Types)' is ignored.

Attachments Settings
====================

All of the settings for 'Attachments' are controlled via the
component manager. To access these settings, go to the administrative
back end and select "Attachments" under the "Component" menu.  Click
on the "Parameters" button on the right end of the tool bar and you will see
a series of parameters for this extension. These parameters include
the following:

* **Who can see attachments:** This setting controls
  who will be able to see the links for the attachments. There are
  three options:

  1.  '*Any logged-in user*'. - If this option is selected, only
      users who are logged into the website will be able to see the links
      to the attachments.
  2.  '*Anyone*' - If this option is selected, the links to the
      attachments will be visible to anyone visiting the website, whether
      they are logged in or not (even in 'secure' mode).
  3.  '*No one*' - If this option is selected, the attachments list and
      links to download the attachments will NOT be visible to normal
      visitors to the website (on the front end), whether they are logged
      in or not.  In secure mode, this prevents downloading attachments
      from the front end.  Administrators, however, will still see the
      attachments list and be able to download the files even if 'no one'
      is selected.

* **Who can add attachments:** This setting controls who is able to add
  attachments to articles or other content elements. There are four options:

  1.  '*Article author only*' - The links to upload and edit attachments will only
      be visible to the author of the parent article/content item (as well as
      other users with higher permissions such as
      editors/publishers/administrators). 
  2.  '*Editor and above*' - The links to upload attachments will only be
      visible to users with Editor permissions and above.
  3.  '*Any logged-in user*' - The links to upload attachments will be
      visible to any user who is logged in.
  4.  '*No one*' - If this option is selected, the "Add Attachments" link
      to upload the attachments will NOT be visible to normal visitors to
      the website (on the front end), whether they are logged in or not.
      In secure mode, this prevents uploading attachments from the front
      end.  Administrators, however, will be able to see the "Add
      attachments" link and be able to upload files even if 'no one' is
      selected.

* **Attachments published by default:** This 'auto
  publish' feature controls whether new attachments are published by
  default when they are added. If 'Yes' is selected, when attachments
  are added, they will published immediately and will be visible to users. If
  'No' is selected, new attachments will not be published by default.
  An administrator will need to publish them from the administrative back end
  before the attachments will be available.
* **Auto Publish Warning:** If the auto-publish option is
  disabled (see previous option), you may wish to inform those adding
  attachments how they can get their attachment published. You can insert an
  appropriate message here.  If this field is empty, a general system message
  will be added suggesting that they contact their system administrator to
  any newly uploaded attachments published. 
* **Show titles:** If set to 'Yes', a row of titles will be
  added above the list of attachments describing what is in each column.
* **Show attachment description:** This setting controls
  whether the attachment description is shown in the list of attachments.
* **Show attachment uploader:** Show the username of the
  one who uploaded the attachment.
* **Show file size:** This setting controls
  whether the attachment file size is shown in the list of attachments.
* **Show number of downloads:** This setting controls
  whether the number of downloads is shown in the list of attachments.

  .. warning:: This option only works in secure mode!
     In non-secure mode, files are maintained as static files and accessed
     directly, without going through Joomla! code.  Therefore it is impossible
     to update the number of downloads for a file when it is accessed this way.
     So the display of the number of downloads will only work in secure mode
     when this option is set to 'Yes'.

* **Show file modification date:** If this setting
  is 'Yes', the modification date for the file will be added to the
  attachment list for articles that have attachments. If 'No' is
  selected, no date will be added to the attachment list.
* **Format string for modification date:** You may
  select the format for the modification date by using the format
  used by the PHP strftime() function.  Search the web with
  'PHP strftime' for examples.  The default format (%x %H:%M)
  gives dates with 24-hour time like 4/28/2008 14:21.  To
  remove the time of day part, leave out the "%H:%M" part.  Note
  that MS Windows and Linux PHP implementations may differ in
  some of the codes that they support.

* **Attachments list order:** This option allows you to specify the order in
  which attachments will be listed in the attachments lists.  Most of the
  options are self-explanatory:

  1.  '*Filename*' - If this option is selected, the attachments will be
      sorted alphabetically by the filename. 
  2.  '*File size(smallest first)*' 
  3.  '*File size(largest first)*' 
  4.  '*Description*' 
  5.  '*Display filename or URL*' - All attachments that have blank
      display filenames will appear before the ones with display filenames and
      will be sorted by their filenames.  
  6.  '*Uploader*' - Sort by the name of the user who uploaded the attachment. 
  7.  '*Creation date (oldest first)*' 
  8.  '*Creation date (newest first)*' 
  9.  '*Modification date (oldest first)*' 
  10. '*Modification date (newest first)*' 
  11. '*Attachment ID*' - If this option is selected, the
      attachments will be sorted by the attachment ID.  This has the effect of
      ordering the attachments in the order they were created.
  12. '*User-defined field 1*' 
  13. '*User-defined field 2*' 
  14. '*User-defined field 3*' 

* **Name for user-defined field 1-3:** If you have some
  additional information about each attachment that you wish to add, the
  'Attachments' extension allows you to defined up to three optional user-defined
  fields.  To create a new field, insert the name for it in one of the three
  entries.  Clear the name to disable the display and editing of this field.
  The user-defined fields will be shown in the order listed here.  The maximum
  length of each user-defined field name is 40 characters.  The data in these
  fields may be up to 100 characters long. 

  .. hint:: If you add an asterisk to the end of a user-defined field name, it
     will not be displayed on the front end.  It will be visible when an
     attachment is edited on the front end and always visible in the back
     end.  This hidden user-defined field can be used to order attachments in
     an arbitrary order by puttting integer values in the field.

* **Maximum filename length:**
  The maximum filename length for attachments list.  Filenames longer than
  this will be truncated and put into the display filename (for display purposes
  only, the actual filename will not be changed).  A value of 0 means the
  filename length is unlimited by this option (the filename field in the attachments
  database table is limited to 80 characters).   Note: If display filenames are truncated
  by this option, the truncated filename will be inserted into the "display filename"
  field.  This option only affects attachments added after this option is set.
* **Where should attachments be placed?** This option controls
  the location in the article (or content item) the list of attachments will be placed.
  This option applies to all attachments lists:

     - '*At the beginning*'
     - '*At the end*'
     - '*Custom placement*' - With this option, the attachments list will
       appear in the article (or content item) where ever the special tag:
       {attachments} occurs.  

       .. warning:: In custom placement mode, any article (or content item)
          that does not include this tag will display its the attachments list
          at its end.

       In this mode, when editing an article, section, or category in the back
       end, an extra button will be displayed: [Insert {attachments} token].
       Position the cursor where you want the custom placement token and use
       this button to insert the token.  This button will add surrounding HTML
       tags to hide the token when it is not replaced (eg, when the
       attachments list is not supposed to be visible).  In HTML, the token
       looks like this with the surrounding tags to hide it::

         <span class="hide">{attachments}</span>

       In the back end editors, you will see the {attachments} tag but not the
       HTML 'span' tags unless you switch to HTML mode.  In the front end, you
       will never see the {attachments} tag unless the insert_attachments_tag
       plugin is disabled.  If you wish to remove the {attachments} token, you
       may want to use the "HTML" view mode in the editor to make sure that
       you also delete the surrounding span tags.
     - '*Disabled (filter)*' - This option will disable the display of
       attachments lists and suppress the display of any {attachments}
       tags in articles or content items.
     - '*Disabled (no filter)*' - This option will disable the display of
       attachments lists and will not suppress the display of any
       {attachments} tags in articles (or content items).
* **CSS style for attachments tables:** To override the CSS
  styling of attachments lists, specify your own style name here.  The default
  style name is 'attachmentsList'.  See  the section `CSS Styling of Attachment Lists`_.
* **URL to register:** If a special URL is needed to register new users,
  insert that URL here.  This option might be useful if a special login page has been created.
* **File link open mode:**
  This mode how the links to attachment files will be opened.  'In same window'
  means the file will be opened in the same browser window.  'In new window'
  means the file will be opened in a new window.  In some browsers, using the
  'In new window' option will actually open the attachment in a new tab.
* **Subdirectory for uploads:** The 'Attachments'
  extension code will put files into this subdirectory under the top
  of the Joomla site.  The default is 'attachments'.
  Note that if this subdirectory is changed, it will only affect future
  uploads.  Previously uploaded files will stay in the old subdirectory
  and records in the attachments database will still point to those files.
  If you wish to move the files from the old subdirectory to the new
  subdirectory, you will need move the files and then update their
  entries in the attachments database table manually.
* **Custom titles for attachments lists:** By default, the 'Attachments'
  extension inserts the title "Attachments:" above the list of attachments for
  each article or content item (if it has attachments). In some cases, you may
  prefer using some other term for specific articles or content items.  You may
  specify the exact term you would like to use on an item-by-item basis. For
  example, if you would like article 211 to use the custom title "Downloads:",
  then add this to this setting: '211 Downloads' (without the quotes). Use one
  entry per line.  For other types of content items, use the form:
  'category:23 This is the title for category 23' where 'category' can be
  replaced by the name of the content item entity.  The example for articles
  above could have been done with 'article:211 Downloads'.  Note that an entry
  without a numeric ID at the beginning will be applied to all content items.
  So it is good practice to put such global overrides first in the list and
  then override the item-by-item custom titles afterwards.
   
  Note: If you wish to change the titles used for attachments lists globally,
  you may edit the translations file entry 'ATTACHMENTS TITLE' in the translation
  files::

      administrator/language/qq-QQ/qq-QQ.plg_frontend_attachments.ini

  where qq-QQ refers to the language designator code such as en-GB for English.
  (If you are not familiar with Joomla! translation files, find the line that
  has 'ATTACHMENTS TITLE' on left side of the '=' sign.  Edit anything to the
  right of the '=' sign.  Do not change anything to the left of the '=' sign.)
* **Hide Attachments for:**
  Comma-separated list of keywords or Sections/Categories of articles for
  which the attachments list should be hidden. Five special keywords may be
  used: 

  - 'frontpage' to suppress displays of attachments on the front page,

  - 'blog' to suppress displays of attachments on any page using the 'blog'
    layout,

  - 'all_but_article_views' to allow displays of attachments only in
    article views, 

  - 'always_show_section_attachments' to enable displaying
    section attachments when 'all_but_article_views' is given, and

  - 'always_show_category_attachments' to enable displaying category attachments
    when 'all_but_article_views' is given. 

  Omit quotes when entering the keyword options.  
  **The 'frontpage' option should be honored by all content types, but content
  types other than articles, sections, and categories may or may not honor the
  'all_but_article_views' option and the other options.** Article
  Section/Category ids should be entered as numeric section and category IDs
  separated with a slash(/): Section#/CategoryNum, SectionNum/CategoryNum.
  Specify just 'SectionNum' to cover all Categories within the Section.
  Example: 23/10, 23/11, 24
* **Timeout for checking links:**
  Timeout for checking links (seconds).  Whenever a link is added as an
  attachment, the link is checked directly (you can disable this check in the
  form).  If the link can be accessed before the timeout, the file size and
  other information about the link is retrieved.  If not, generic information
  is used.  To disable the check, enter 0.
* **Superimpose URL link icons:**
  Superimpose URL link icons over the file attachment icon for each
  attachment to indicate it is a URL.  Valid URLs are shown with arrows and
  invalid URLs are shown with a red line across the file type icon (bottom
  left to top right).
* **Suppress obsolete attachments (in back end):**
  Set the default for suppressing *obsolete* attachments in the administrative
  back end.  In this context, *obsolete* attachments are ones attached to
  unpublished or trashed parents. You can override this using the 'Show
  attachments for' drop-down menu on the right just above the list of
  attachments (on the same line as the filter).  When you use the drop-down
  menu to control which attachments are visible, the system remembers that
  setting until you log out as administrator.  So changing this parameter may
  not seem to have an effect.  This parameter setting will come into effect
  the next time you log in as administrator.
* **Secure attachment downloads:** 
  By default, the 'Attachments' extension saves attachment files in a publicly
  accessible subdirectory.  If you choose the *secure* option, the directory
  in which the attachments are saved will be made publicly inaccessible.  The
  download links for the attachments in the front end will download the
  attachment files but will not be direct links.  This will prevent access
  unless users have appropriate permissions.  If *secure* downloads are not
  selected, the links to the attachments will be shown as the options above
  indicate, but the files will still be accessible to anyone if they know the
  full URL, since the subdirectory is public.  The *secure* option prevents
  access to users without appropriate permissions even if they know the full
  URL, since this option prevents public access to the attachments
  subdirectory.  In *secure* mode, the option "Who can see" can set to
  'Anyone' and anyone will be able to see and download the attachments.
* **List attachments in secure mode:**
  List attachments in secure mode, even when users are not logged in unless
  'Who can see attachments' is set to 'No one'.  The 'Who can see
  attachments' option still controls whether attachments can be downloaded,
  even in secure mode.  This option is only enforced in secure mode.
* **Download mode for secure downloads:** 
  This option controls whether files should be downloaded as separate files or
  displayed in the browser (if the browser can handle that type of file).
  There are two options:

     - *'inline'* - In this mode, files that can be displayed by the browser
	 will be displayed in the browser (such as text files and images).

     - *'attachment'* - With the 'attachment' mode, files will always be
	 downloaded as separate files.

  In either case, files that can't be displayed in the browser will be
  downloaded as external files.

Display Filename or URL
=======================

Normally, when files are uploaded (or URLs are installed) and listed in a list
of attachments, the full filename (or URL) is shown as a link to download the
attachment.  In some cases, the filename (or URL) may be too long for this to
work nicely.  In the upload form, there is another field called "Display
Filename or URL" in which the person uploading the file can insert an
alternative filename (or URL) or label to display instead of the full filename
(or URL).  For instance, some abbreviation of the filename could be added in
this field.  The field may be edited in the administrative back end when
attachments are edited.  Note: There is an option called "Maximum Filename or
URL Length" in the 'Attachments' extension options.  It can be set to automatically
truncate uploaded displayed filenames; the resulting truncated filename will
be inserted into the "Display Filename or URL" field.

Attaching URLs
==============

A new feature in 'Attachments' version 2.0 is the ability to "attach" URLs to
content items.  When you bring up one of the "Add attachment" dialog boxes,
you will see a button labeled as "Enter URL instead".  If you click on it you
will get an entry field for the URL and see two options:

* **Verify URL existence?** - In order to determine the file type of the
    URL (to pick a suitable icon), the code queries the server for basic
    information about the file including the file type and size.  In some
    cases, the server will not respond to these requests even though the
    URL is valid.  By default, Attachment will not accept URLs that have
    not been validated by the server.  But if you know the URL is valid,
    you can uncheck this option and force the 'Attachments' extension to
    take the URL--but there are no guarantees the file type or file size
    will be correct.  Note that the server will be queried whether or not
    this option is selected.

* **Relative URL?** - Normally you will enter URLs prefixed with 'http...' to
    indicate an full website URL.  If you wish to point to files/commands
    relative to your Joomla installation, use the 'relative' option.

The URLs are shown with the file-type icon and overlaid with an arrow
(indicating that it is a good link) or an red diagonal slash (indicating that
it could not be validated).  When you edit a URL, you can change whether the
link is valid or not to get the overlay you wish.  Also note that URL overlays
can be disabled entirely using the main **Superimpose URL link icons**
parameter.  There are several useful commands relating to URLs (and files) in
the "Utilities" command in the back end.

What Can Files Be Attached To?
==============================

Besides attaching files or URLs to articles, it is now possible to
attach files or URLs to other types of content items such as Sections
and Categories (see below).  If appropriate 'Attachments' plugins are
installed, it may be possible to attach files or URLs to a wide variety
of content items such as user profiles, shopping cart product
descriptions, etc.  Basically any content item that is displayed on the
front end and uses the content event ``'onPrepareContent'`` can host
attachments (if a suitable 'Attachments' plugin is installed).  Content
items that invoke content events are typically items that have content
to be displayed (such as articles) or have descriptions that will be
displayed.

Attaching Files or URLs to Section or Category Descriptions
-----------------------------------------------------------

With this version of attachments, users can attach files to Section and
Category descriptions.  These descriptions are generally only visible on
Section or Category Blog pages, if the basic parameter 'description' is set to
*Show* (via the Menu Editor).  Attachments may be added to Section or Category
descriptions in the Section or Category editors.

If you wish to learn more about how to develop a new Attachment plugin, there
is a manual that is available as part of this 'Attachments' installation:

* `Attachments Plugin Creation Manual 
  <../en-GB/plugin_manual/html/index.html>`_ (in English)


CSS Styling of Attachment Lists
===============================

The lists of attachments on the front end are done using a special
'div' that contains a table for the attachments. The table has
several different CSS classes associated with it to allow the website
developer the flexibility to customize the appearance of the table. Look in
the attachments plugin file CSS file (in plugins/content/attachments.css) for
examples. If you wish to change the style, consider copying the original
styles into the end of the same file and renaming 'attachmentsList' in the
copied section to something of your choice.  Edit the 'Attachments' parameter
(in the  component manager) and change the parameter *attachments table style*
to the new class name. Then modify the class definitions in your copied section
appropriately. This approach will allow you to quickly revert to the original
style by changing the plugin parameter *attachments table style* back to
its default, 'attachmentsList'. This also has the advantage that the
section of modified styles can be copied to a file and easily brought back in
when the version of 'Attachments' is upgraded. This could also be done via a
CSS @import command.

File Type Icons
===============

The 'Attachments' extension adds an icon in front of each attachment in the
list of attachments. If you wish to add a new icon type, follow these steps:

1. Add an appropriate icon in the directory 'media/attachments/icons', if an
   appropriate icon is not already there;

2. Edit the file 'components/com_attachments/file_types.php' and add an
   appropriate line to the static array $attachments_icon_from_file_extension
   which maps a file extension to an icon name (all in the
   media/attachments/icons directory). If this does not work, you may need to
   add an appropriate line to the array $attachments_icon_from_mime_type.

3. Don't forget to make copies of the icon file and the updated file_types.php
   to some directory outside of the website directories before upgrading the
   version of 'Attachments' in the future.

Translations
============

This extension provides translation capabilities and supports the
following languages (besides English).  Note that some of these languages
packs are in the process of being updated for 'Attachments' version 2.0 and
not available yet for Attachments 2.0.  Anyone needing the language packs for
1.3.4 should contact the author directly.

Thanks to these translators (available versions shown in parentheses):

* **Bulgarian:** by Stefan Ilivanov (being updated to 2.0)
* **Catalan:** by Jaume Jorba (2.0)
* **Chinese:** Traditional and simplified Chinese translations by baijianpeng (白建鹏) (being updated to 2.0)
* **Croatian:** Tanja Dragisic (1.3.4)
* **Czech:** by Tomas Udrzal (1.3.4)
* **Dutch:** by Parvus (2.0)
* **Finnish:** by Tapani Lehtonen (2.0)
* **French:** by Marc-André Ladouceur (2.0) and Pascal Adalian (1.3.4)
* **German:** by Bernhard Alois Gassner (2.0) Michael Scherer (1.3.4)
* **Greek:** by Harry Nakos (being updated to 2.0)
* **Hungarian:** Formal and informal translations by Szabolcs Gáspár (1.3.4)
* **Italian:** by Piero Mattirolo (2.0) and Lemminkainen and Alessandro Bianchi (1.3.4)
* **Norwegian:** by Roar Jystad (2.0) and Espen Gjelsvik (1.3.4)
* **Persian:** by Hossein Moradgholi and Mahmood Amintoosi (2.0)
* **Polish:** by Sebastian Konieczny (2.0) and Piotr Wójcik (1.3.4)
* **Portuguese (Brazilian):** by Arnaldo Giacomitti and Cauan Cabral (being updated to 2.0)
* **Portuguese (Portugal):** by José Paulo Tavares (2.0) and Bruno Moreira (1.3.4)
* **Romanian:** by Alex Cojocaru (2.0)
* **Russian:** by Sergey Litvintsev (2.0) and евгений панчев (Yarik Sharoiko) (1.3.4)
* **Serbian:** by Vlada Jerkovic (being updated to 2.0)
* **Slovak:** by Miroslav Bystriansky (1.3.4)
* **Slovenian:** by Matej Badalič (2.0)
* **Spanish:** by Manuel María Pérez Ayala (2.0) and Carlos Alfaro (1.3.4)
* **Swedish:** by Linda Maltanski (2.0) and Mats Elfström (1.3.4)
* **Turkish:** by Kaya Zeren (2.0)

Many thanks to these translators!  If you would like to help translate
the extension to any other language, please contact the author (see the
`Contact`_ section at the end).

Warnings
========

* **If you have attachment files that are sensitive or private, use the
  *Secure attachment downloads* option!** If you do not use the secure option, 
  the attachment files are saved in a public subdirectory and are accessible
  to anyone that knows the full URL.  The *secure* option prevents access by
  anyone that does not have appropriate permissions (as determined by the
  options above).  See the discussion of the *Secure attachment downloads*
  option above for more detail.
* Every time a file is uploaded, the existence of the upload subdirectory is
  checked and it will be created if if it does not exist.  By default the
  subdirectory for uploaded files is 'attachments' in the root directory of
  your web site files.  The name of the subdirectory can be changed using the
  'Subdirectory for uploads' option. If the 'Attachments' extension is unable
  to create the subdirectory for uploads, you must create it yourself (and you
  may have problems uploading files).  Make sure to give the subdirectory
  suitable permissions for uploading files.  In the Unix/Linux world, that is
  probably something like 775.  Note the process of creating the upload
  subdirectory may fail if the top level directory of your website has
  permissions that prevent the web server (and PHP) from creating
  subdirectories.  You may need to loosen the permissions temporarily to allow
  the subdirectory to be created by uploading attachments.
* If this extension does not permit you to upload specific types of files
  (such as zip files), be aware that the extension respects the restrictions
  placed by the Media Manager on types of files permitted to be uploaded. This
  is to prevent uploading of potentially harmful types of files such as html or
  php files. The administrator can update the Media Manager settings to add
  specific file types by going to the "Global Settings" item under the "Site"
  menu, selecting the "System" tab, and added the appropriate file extension and
  Mime type to the lists under the "Media Manager" section.
* If you cannot see the attachments in the front end, there are several
  possible reasons:

     - The attachment is not published.  You can change this in Attachments
       manager page in the back end.
     - The parent article or content item is not published.
     - The option 'Who can see attachments' is set to 'logged-in' and you are
       not logged in on the front end. 
     - Or the option 'Who can see attachments' is set to 'no one'. This can be
       changed via the Parameter editor in the component manager.
     - The 'Content - Attachments' plugin is not enabled.  Use the plugin manager
       to enable it. 
     - In the 'Content - Attachments' (via the plugin manager), the access
       level is not set to 'Public'. 
     - If your site uses caching, try clearing the caches and refreshing the
       page. 
* If you encounter limits on the sizes of files that you attempt to upload,
  try adding the following lines to the .htaccess file in the root of
  your Joomla! website::

     php_value upload_max_filesize 32M
     php_value post_max_size 32M

  where you may change the 32M (megabytes) value to whatever you wish as the maximum
  upload file size.
* 'Attachments' now supports "attaching" URLs to content items.  If your server
  is Windows Vista and you encounter problems attaching URLs that involve
  ``localhost``, this is a known problem related to IPv4 and IPv6 conflicts.
  To fix it, edit the file::

       C:\Windows\System32\drivers\etc\hosts

  Comment out the line that has ``::1`` on it.  Note that ``hosts`` is a
  hidden system file and you may need to modify your folder options to show
  hidden files to see and edit it.
* If you have difficulties attaching files that have unicode characters (such
  as Russian/Cyrillic characters), use the *secure* option.  Filenames with
  unicode characters should work properly on Linux servers, but do not always
  work correctly on Windows servers in non-secure mode.
* 'Attachments' now supports attaching files to articles while they are being
  created in the Article editor.  There is one limitation to this.  New
  attachments are in a state of "limbo" after the file is uploaded and before
  the article is actually saved for the first time.  During this (hopefully
  brief) limbo period, the new attachments are identified by user id only.  So
  if more than one person is using the same user account and they create
  articles at the same time and add attachments at the same time, there is no
  guarantee that the attached files will end up with the correct article.
* In the back end, sometimes when you execute one of the Utility commands, you
  may get a warning that the browser needs to resend the request.  This is
  harmless, so click [Ok] and the command will execute.
* The Utility command to "Regenerate system filenames" works for migration
  from windows to Linux servers.  It also works for migraton from Linux to
  Windows servers with a couple of potential problems:

     - When you copy your files to your Windows server, you need to verify
       that the atthachments directory (usually 'attachments') and all files
       within it are writable by the Joomla web server.
     - You may have problems porting files that have unicode characters in
       their filenames because the archiving/unarchiving software has problems
       with the unicode filenames (on the Windows side).  You may need to save
       those files, delete the corresponding attachments, and then re-attach
       them.
* There is a help forum and a 'Frequently Asked Questions' forum for the
  'Attachments' extension that is hosted on the joomlacode.org website.  If
  you encounter a problem that is not covered in this help page, please
  consult the forums:

     - `Attachments Forums at
       http://joomlacode.org/gf/project/attachments/forum/ 
       <http://joomlacode.org/gf/project/attachments/forum/>`_


Upgrading
=========

Upgrading is much easier now.  Simply install the new version of 'Attachments'.

* *[This step is optional but highly encouraged to make sure you have
  a backup of the attachments database in case something goes wrong.]*
  Use `phpMyAdmin <http://www.phpmyadmin.net/home_page/index.php>`_
  (or other SQL editing tool) to save the contents
  of the jos_attachments table (Use the 'Export' option with
  'Complete' inserts for data (not 'Extended' inserts).  You should also
  back up the uploaded attachments files (usually in the 'attachments'
  directory )
* **You do not need to uninstall the previous version of Attachments.** This
  has been tested with 2.0 and 1.3.4 (but not with earlier versions).
* If you wish to retain any existing attachments, you do not need to do
  anything.  Simply install the new version and it will update everything
  appropriately. 
* If you do not wish to keep existing attachments, delete them all first (in
  the administrative back end).
* The multi-installer will install all necessary components and plugins and
  enable all plugins.  If do not want any of the plugins enabled, install
  first and then disable plugins as desired.  If there is a problem with
  the installation, you may need to do a manual piece-by-piece installation.
  See the INSTALL file included within the main installation zip file for
  directions. 


Acknowledgements
================

Many thanks for the following contributors or resources:

* The book *Learning Joomla! 1.5 Extension Development: Creating Modules,
  Components, and Plugins with PHP* by Joseph L. LeBlanc was very helpful
  in creating the 'Attachments' extension.
* The icons for the file types were derived from several sources, including:
    - `The Silk icons by Mark James (http://www.famfamfam.com/lab/icons/silk/) <http://www.famfamfam.com/lab/icons/silk/>`_
    - `File-Type Icons 1.2 by John Zaitseff (http://www.zap.org.au/documents/icons/file-icons/sample.html) <http://www.zap.org.au/documents/icons/file-icons/sample.html>`_
    - `Doctype Icons 2 by Timothy Groves (http://www.brandspankingnew.net/archive/2006/06/doctype_icons_2.html) <http://www.brandspankingnew.net/archive/2006/06/doctype_icons_2.html>`_
    - `OpenDocument icons by Ken Baron (http://eis.bris.ac.uk/~cckhrb/webdev/) <http://eis.bris.ac.uk/~cckhrb/webdev/>`_
    - `Sweeties Base Pack by Joseph North (http://sweetie.sublink.ca) <http://sweetie.sublink.ca>`_

  Note that many of the 'Attachments' icons were modified from the original
  icon images from these websites.  If you would like the original versions,
  please download them from the websites listed above.
* Many thanks to Paul McDermott for generously donating the search plugin!
* Thanks to Mohammad Samini for donating some PHP code and CSS files to
  improve 'Attachments' displays in right-to-left languages.
* Thanks to Florian Tobias Huber for donating fixes to improve attachments
  displays with caching is enabled.
* Thanks to Manuel María Pérez Ayala for suggesting how to create the
  integrated multi-installer.  The multi-installer uses the Joomla
  installer API to automatically install the component and all the
  plugins in one simple step.  My understanding is that this technique
  was originally developed by JFusion.
* Thanks to Ewout Weirda for many helpful discussions and suggestions in
  the development of the 'Attachments' extension.

Contact
=======

Please report bugs and suggestions to `jmcameron@jmcameron.net <mailto:jmcameron@jmcameron.net>`_
