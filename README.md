# Schema for redirect urls for various developer applications and user interfaces
**The schema is as follows**
* For now consider a yo link
 * `yo/<monitoring system name.sub component.subsubcomponent>-<logtype.sublogtype>-<app name.sub app name.sub sub app name>-<environment>`
 * All the above values in the <> brackets are mandatory and defaults cannot be assumed for clarity and portability
* Reserved keywords (which cannot be used by the user using this schema) are
  * `-` used to separate entities
  * `.` used to add granularity to app specific details or monitoring specific details
* Possible values user can enter. No other set of characters is allowed other than the mentioned set. This strict adherence to a given character set makes things simple and clear
  * `[a-z][0-9][.][ _ ]`
  * use  `_` if the names get too long and difficult to read but avoid as much as possible as the idea is to be simple, clear and precise
* While writing sub app names only `[a-z][0-9]` set is to used. For example
  * `yo/splunk-access-picknroll-dev`
  * `yo/splunk-error-picknroll-test`
  * `yo/nimbus-info-slick-stage`
  * `yo/nimbus-info-slick-prod`
* <environment> needs to be from the below set
  * `[int, dev, stage, burn, perf, prod]`
  * geo locations of envs must be written as
    * `yo/splunk-access-picknroll-prod.gq1`
    * `yo/splunk-access-picknroll-dev.bf1`
    * `yo/splunk-access-picknroll-perf.sg3`
* If geographic locations are required for app and app.subapp, they must be put at the end of the string only
  * `app.gq1`
  * `app.subapp.gq1`
  * `app.ne1.component.gq1.subcomponent.sg3.subsubcomponent.bf1` (this is bad as it is an indication of a complex system and complexity increases bugs)
# Good to haves (strongly recommended)
* The urls these redirects represent should be lightweight and easy to load, for e.g
  * A spunk log url with time query as 15 min instead of 24 hours or 1 week
* Try to avoid the names being too long and difficult to read as only [a-z] can be used. a option is to use `_` but this should be avoided as much as possible. More information does not necessarily mean more clarity
* Avoid makes these redirect urls specific at all costs, for example
  * `yo/splunk-error-picknroll.customquery1-prod`
  * `yo/splunk-error-picknroll.customquery2-prod`
* Avoid having multiple names for the same app at least when creating these redirect urls, one name increases clarity
  * pnr
  * picknroll
* Avoid at all costs to add hacks here since hacks were added in the respective application, these redirect urls are meant to be universal in every sense and not just your team
* If that is the use case is say logs for a particular production box then using this probably not a good idea incase a large group of people need it. Ideally actual boxes should be abstracted away from the developer and the debug application should take care of narrowing down on the box in its UI. As an alternative a google doc can solve this use case. For example
  * In splunk you can change the hostname to a specific k8s pod, but a specific redirect url should not be created just for this purpose
* If it’s something extremely custom and a lot of people need it, u can do this for e.g
  * `yo/google.doc-info-<appname>-<env>`
  * Add all the custom stuff in the google doc, the users have to do one extra click but a doc is better as u can add notes, comments and be more verbose
* Common apps like google docs, google sheets, splunk, yamas or some other debug app can be added to the reserved keyword list and only those should be used to avoid using multiple names for the same app across teams. For example
  * `splunk`
  * `google.doc`
  * `google.sheet`
* Have standard debug levels
  * info
  * error
