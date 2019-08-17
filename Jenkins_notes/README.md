<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Jenkins_logo.svg/556px-Jenkins_logo.svg.png" alt="Bazel logo" height="42px" width="42px" align="left"><br>

# Jenkins Notes
<div>
    <a href="https://github.com/NaPiZip/Tipps-and-tricks">
        <img src="https://img.shields.io/badge/Document%20Version-0.0.1-brightgreen"/>
    </a>
    <a href="https://www.microsoft.com">
        <img src="https://img.shields.io/badge/Windows%2010%20x64-10.0.17134%20Build%2017134-blue.svg"/>
    </a>
    <a href="https://jenkins.io/">
        <img src="https://img.shields.io/badge/Jenkins%20Version-2.176.2-blue"/>
    </a>
</div>

## How to get a list of all installed plugins
This section describes how to get a list of installed jenkins plugins, this can be used to created a `plugins.txt` file, for details see the Docker Jenkins [manual](https://github.com/jenkinsci/docker/blob/master/README.md).

1. Start Jenkins
2. Login using a web browser.
3. Navigate to the following URL in your browser:
```
http://<jenkins-url>/script
```
4. Execute the following Java code:
```
List<String> jenkinsPlugins = new ArrayList<String>(Jenkins.instance.pluginManager.plugins);
jenkinsPlugins.sort { it.displayName }
              .each { plugin ->
                   println ("${plugin.shortName}:${plugin.version}")
              }
```
5. Examine the results.
```
ant:1.9
apache-httpcomponents-client-4-api:4.5.5-3.0
authentication-tokens:1.3
...
```

## Contributing
To get started with contributing to my GitHub repository, please contact me [Slack](https://join.slack.com/t/napi-friends/shared_invite/enQtNDg3OTg5NDc1NzUxLWU1MWNhNmY3ZTVmY2FkMDM1ODg1MWNlMDIyYTk1OTg4OThhYzgyNDc3ZmE5NzM1ZTM2ZDQwZGI0ZjU2M2JlNDU).
