Convert Attachments to Chatter Files
====================================

<a href="https://githubsfdeploy.herokuapp.com?owner=douglascayers&repo=sfdc-convert-attachments-to-chatter-files">
  <img alt="Deploy to Salesforce"
       src="https://raw.githubusercontent.com/afawcett/githubsfdeploy/master/src/main/webapp/resources/img/deploy.png">
</a>

A batchable apex class that converts attachments into chatter files to take advantage of more sophisticated sharing and file revisions.


Usage
-----
In Salesforce, open the Developer Console and run this anonymous apex snippet:

`Database.executeBatch( new ConvertAttachmentsToFilesBatchable(), 200 );`

If you run into governor limits, you may need to reduce the batch size from 200.


Background
----------
In the Winter 16 release, Salesforce introduces a new related list called Files.
This new related list specifically shows only Chatter Files shared to the record.
Seeing as this is the future of Salesforce content, you may want to plan migrating
your existing Attachments to Chatter Files. That is the function of this class.

Migrating to Files instead of Attachments is a good idea because Chatter Files
provide you much more capabilities around sharing the file with other users, groups, and records.
It also supports file previews and revisions. It is the future of managing content in Salesforce.

Learn more at:
* http://docs.releasenotes.salesforce.com/en-us/winter16/release-notes/rn_chatter_files_related_list.htm#topic-title
* https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_contentversion.htm

Example page layout with the new **Files** and **Notes** related lists added:
![screenshot](/images/related-lists-pre-conversion.png)

Example results after running the conversion code:
![screenshot](/images/related-lists-post-conversion.png)

Pre-Requisites
--------------
To simplify the conversion code, two custom fields need to be added to the ContentVersion object to store the original attachment id and its parent id. **If you click the Deploy to Salesforce button above then these fields are created for you.**

1. Go to **Setup | Customize | Salesforce Files | Fields**
2. Create new field Text(255) named **Original Attachment ID**
3. Create new field Text(255) named **Original Attachment Parent ID**

![screenshot](/images/content-version-custom-fields.png)


Credits
-------
Code adapted from Chirag Mehta's post on stackoverflow.
http://stackoverflow.com/questions/11395148/related-content-stored-in-which-object-how-to-create-related-content-recor
