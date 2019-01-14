# JitPack Android Monorepo

JitPack defaults to publishing a single artifact with:

- groupId = com.github.User
- artifactId = repo
- version = commit hash

In a mono repo, that format is expaneded to:

`user:repo:module:version`

> mvn install:install-file -Dfile=mylib/build/outputs/aar/mylib-debug.aar -DgroupId=group1 -DartifactId=a1 -Dversion=SNAPSHOT -Dpackaging=aar

In this example, the library is published as `a1-1a3f4669dc.aar`. The artifactId is the module name. Note that jitpack will *only* respect module names if there is more than one artifact published to maven.

# Example

Given this jitpack.yml

```yaml
install:
   - ./gradlew clean build
   - mvn install:install-file -Dfile=mylib/build/outputs/aar/mylib-debug.aar -DgroupId=group1 -DartifactId=a1 -Dversion=SNAPSHOT -Dpackaging=aar
   - mvn install:install-file -Dfile=mylib/build/outputs/aar/mylib-release.aar -DgroupId=group2 -DartifactId=a2 -Dversion=SNAPSHOT -Dpackaging=aar
```

The libs may be added via commit hash:

```gradle
implementation 'com.github.bootstraponline.jitpack-tmp:a1:1a3f4669dc'
implementation 'com.github.bootstraponline.jitpack-tmp:a2:1a3f4669dc'
```

or via snapshot:

```gradle
implementation 'com.github.bootstraponline.jitpack-tmp:a1:-SNAPSHOT'
implementation 'com.github.bootstraponline.jitpack-tmp:a2:-SNAPSHOT'
```
