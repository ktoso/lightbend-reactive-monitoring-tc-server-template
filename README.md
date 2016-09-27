Using a template to add Cinnamon to tcServer
============================================

* Download tc-server.

* clone this template, call it `lightbend-reactive-monitoring-tc-server-template`

* you'll need to download the commercial monitoring java agent "cinnamon":

  * learn here how to set up credentials: https://www.lightbend.com/product/lightbend-reactive-platform/credentials
  * for sbt https://developer.lightbend.com/docs/reactive-platform/2.0/setup/setup-sbt.html
  * for gradle https://developer.lightbend.com/docs/reactive-platform/2.0/setup/setup-gradle.html
  * or maven https://developer.lightbend.com/docs/reactive-platform/2.0/setup/setup-maven.html

* once you have credentials set up, you can download dependencies, including the agent.
  This is best done via a sample project as linked here: https://developer.lightbend.com/docs/monitoring/latest/getting-started/sbt.html
  
* since we want to add the agent to tomcat when starting it, we'll want to make a template that can include the agent:

```
cd WHERE_YOU_CLONED_THIS_REPO
cd lib
cp ~/.ivy2/cache/com.lightbend.cinnamon/cinnamon-agent/jars/cinnamon-agent-2.0.0.jar .
```

* now the template is prepared.

* Link it to where you build your tc-server's. Could be on a remote box or locally:

```
cd tc-server-developer-3.2.0.RELEASE/templates 
ln -s WHERE_YOU_CLONED_THIS_REPO lightbend-reactive-monitoring-tc-server-template 
```

* Then you can create new servers using:

```
# ktoso @ 月~/code/tc-server-developer-3.2.0.RELEASE
./tcruntime-instance.sh create --force --template base \
    --template lightbend-reactive-monitoring-tc-server-template \
    lightbend-monitoring-example
```

Apps can now be monitored using Cinnamon, refer to the docs for more info:
https://developer.lightbend.com/docs/monitoring/latest/
