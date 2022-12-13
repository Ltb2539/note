查看Androidmainfset.xml,转换为txt

```shell
java -jar AXMLPrinter2.jar AndroidManifest.xml >> AndroidManifest.txt
```

删除指定activity

节点 节点名称 原文件 删除后文件

```shell
java -jar AXMLEditor2.jar -tag -r activity io.dcloud.PandoraEntry AndroidManifest.xml AndroidManifest1.xml
```

