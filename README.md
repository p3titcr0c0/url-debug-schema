# url-debug-schema
a standard schema for redirect urls for various debug applications used by developers that can be shared across teams


# Schema for redirect urls for various developer applications and user interfaces
**the schema is as follows**
* For now consider a yo link
  *  yo/<monitoring system name.sub component.subsubcomponent>-<logtype.sublogtype>-<app name.sub app name.sub sub app name>-<environment>
  * all the above values in the <> brackets are mandatory and defaults cannot be assumed for clarity and portability
reserved keywords (which cannot be used by the user using this schema) are
  * `-` used to separate entities
  * `.` used to add granularity to app specific details
  * possible values user can enter. No other set of characters is allowed other than the mentioned set. This strict adherence to a given character set makes things simple and clear
  * [a-z][0-9][.]
  * use  `_` if the names get too long and difficult to read but avoid as much as possible as the idea is to be simple, clear and precise
While writing sub app names only [a-z][0-9] set is to used
the given examples uses the yo links
yo/splunk-access-picknroll-dev
yo/splunk-error-picknroll-test
yo/nimbus-info-slick-stage
yo/nimbus-info-slick-prod
<environment> needs to be from the below set
[int, dev, stage, burn, perf, prod]
geo locations of envs must be written as
prod.gq1
prod.bf1
prod.sg3
if geographic locations are required for app and app.subapp, they must be put at the end of the string only
app.gq1
app.subapp.gq1
app.ne1.component.gq1.subcomponent.sg3.subsubcomponent.bf1   (this is bad as it is an indication of a complex system and complexity increases bugs)
good to haves
The urls these redirects represent should be lightweight and easy to load, for e.g
A spunk log url with time query as 15 min instead of 24 hours or 1 week
Try to avoid the names being too long and difficult to read as only [a-z] can be used. a option is to use `_` but this should be avoided as much as possible. More information does not necessarily mean more clarity
Avoid makes these redirect urls specific at all costs, for e.g
yo/splunk-error-picknroll.customquery1-prod
yo/splunk-error-picknroll.customquery2-prod
Avoid having multiple names for the same app at least when creating these redirect urls, one name increases clarity
pnr
picknroll
publishingplatformwebsite
Avoid having multiple names for the same thing at all costs and these redirects are actual urls 
yo/splunk-info
yo/splunk-error
In most cases this means the error log of the application, so just use <error> and not <info> for all cases
Avoid at all costs to add hacks here since hacks were added in the respective application, these redirect urls are meant to be universal in every sense and not just your team
Avoid trying to create urls for different boxes, if that is the use case then using this probably not a good idea incase a large group of people need it. Ideally actual boxes should be abstracted away from the developer and the debug application should take care of narrowing down on the box in its UI.
In splunk u can change the hostname to a specific k8s pod, but a specific redirect url should not be created just for this purpose
If it’s something extremely custom and a lot of people need it, u can do this for e.g
yo/googledoc-info-<appname>-<env>
Add all the custom stuff in the google doc, the users have to do one extra click but a doc is better as u can add notes, comments and be more verbose

